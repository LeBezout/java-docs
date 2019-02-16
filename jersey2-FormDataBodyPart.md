# How to build FormDataBodyPart objects to upload files

For example for testing purpose

## Via FileDataBodyPart

```java
public static FormDataBodyPart buildFileDataBodyPart(File fileToUpload) {
  return new FileDataBodyPart("attached-file", fileToUpload, MediaType.APPLICATION_OCTET_STREAM_TYPE);
}
```

## Via FormDataMultiPart

```java
public static FormDataBodyPart buildFormDataBodyPart(File fileToUpload) throws FileNotFoundException {
  FormDataMultiPart part = new FormDataMultiPart().field("file", new FileInputStream(fileToUpload), MediaType.APPLICATION_OCTET_STREAM_TYPE);
  return part.getField("file");
}
```

## IllegalStateException: Entity instance does not contain the unconverted content

But if we use the `getValueAs` or `getEntityAs` methods on the `FormDataBodyPart` to read the data we're facinf this issue.

:link: [stackoverflow thread](https://stackoverflow.com/questions/14456547/how-to-unit-test-handling-of-incoming-jersey-multipart-requests)

The `BodyPart.getEntityAs` method expects a `BodyPartEntity`....and then it's a little bit touchy: to build a `BodyPartEntity` we must provide a `MIMEPart`, to build a `MIMEPart` we must build a `MIMEMessage` (from `org.jvnet.mimepull` API)!

Here is my solution to deal with this issue :

```java
package com.github.lebezout;

import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.lang.annotation.Annotation;
import java.lang.reflect.Type;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;
import java.util.Map;

import javax.ws.rs.WebApplicationException;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.MultivaluedMap;
import javax.ws.rs.ext.MessageBodyReader;
import javax.ws.rs.ext.MessageBodyWriter;
import javax.ws.rs.ext.ReaderInterceptor;
import javax.ws.rs.ext.WriterInterceptor;

import org.glassfish.jersey.internal.PropertiesDelegate;
import org.glassfish.jersey.media.multipart.BodyPartEntity;
import org.glassfish.jersey.media.multipart.FormDataBodyPart;
import org.glassfish.jersey.media.multipart.FormDataContentDisposition;
import org.glassfish.jersey.message.MessageBodyWorkers;
import org.glassfish.jersey.message.ReaderModel;
import org.glassfish.jersey.message.WriterModel;
import org.jvnet.mimepull.MIMEConfig;
import org.jvnet.mimepull.MIMEMessage;
import org.jvnet.mimepull.MIMEPart;

public final class FormDataBodyPartBuilder {
  private final File dataFile;
  private String contentId = "part";
  private String contentType = "application/octet-stream";
  private String boundary = "boundary";

  private FormDataBodyPartBuilder(final File pFile) {
    dataFile = pFile;
  }
  
  public static FormDataBodyPartBuilder ofFile(final File pFile) {
    return new FormDataBodyPartBuilder(pFile);
  }
  public static FormDataBodyPartBuilder ofFilename(final String pFilename) {
    return new FormDataBodyPartBuilder(new File(pFilename));
  }
  public static FormDataBodyPartBuilder ofPath(final Path pPath) {
    return new FormDataBodyPartBuilder(pPath.toFile());
  }
  
  public FormDataBodyPartBuilder withContentType(final String pContentType) {
    contentType = pContentType;
    return this;
  }
  
  public FormDataBodyPartBuilder withContentId(final String pContentId) {
    contentId = pContentId;
    return this;
  }
  
  public FormDataBodyPartBuilder withBoundary(final String pBoundary) {
    boundary = pBoundary;
    return this;
  }
  
  public FormDataBodyPart build() throws IOException {
    FormDataBodyPart filePart = new FormDataBodyPart();
    filePart.setMediaType(MediaType.valueOf(contentType));
    filePart.setContentDisposition(FormDataContentDisposition.name(contentId).fileName(dataFile.getName()).size(dataFile.length()).build());
    InputStream data = buildInputStreamMessage(dataFile, boundary, contentId, contentType);
    MIMEConfig config = new MIMEConfig();
    config.setParseEagerly(true);
    @SuppressWarnings("resource")
    MIMEMessage message = new MIMEMessage(data, boundary, config);
    final MIMEPart part = message.getAttachments().get(0);
    BodyPartEntity entity = new BodyPartEntity(part);
    filePart.setEntity(entity);
    filePart.setMessageBodyWorkers(getMessageBodyWorkers());
    return filePart;
  }
  
  private static InputStream buildInputStreamMessage(File pDataFile, String pBoundary, String pName, String pContentType) throws IOException {
    // Inspired from https://github.com/javaee/metro-mimepull/blob/master/src/test/java/org/jvnet/mimepull/FileTest.java
    final byte[] predata = ("--" + pBoundary + "\r\nContent-Type: " + pContentType + "\r\nContent-Id: " + pName + "\r\n\r\n").getBytes();
    final byte[] postdata = ("\r\n--" + pBoundary + "--").getBytes();
    final byte[] data = Files.readAllBytes(pDataFile.toPath());
    final byte[] result = new byte[predata.length + data.length + postdata.length];
    int index = 0;
    System.arraycopy(predata, 0, result, index, predata.length);
    index += predata.length ;
    System.arraycopy(data, 0, result, index, data.length);
    index += data.length ;
    System.arraycopy(postdata, 0, result, index, postdata.length);
    return new ByteArrayInputStream(result);
  }
  
  private static MessageBodyWorkers getMessageBodyWorkers() {
    return new MessageBodyWorkers() {
      
      @Override
      public String writersToString(@SuppressWarnings("rawtypes") Map<MediaType, List<MessageBodyWriter>> pArg0) {
        return null;
      }
      
      @Override
      public OutputStream writeTo(Object pArg0, Class<?> pArg1, Type pArg2, Annotation[] pArg3, MediaType pArg4, MultivaluedMap<String, Object> pArg5,
          PropertiesDelegate pArg6, OutputStream pArg7, Iterable<WriterInterceptor> pArg8) throws IOException, WebApplicationException {
        return null;
      }
      
      @Override
      public String readersToString(@SuppressWarnings("rawtypes") Map<MediaType, List<MessageBodyReader>> pArg0) {
        return null;
      }
      
      @Override
      public Object readFrom(Class<?> pArg0, Type pArg1, Annotation[] pArg2, MediaType pArg3, MultivaluedMap<String, String> pArg4, PropertiesDelegate pArg5,
          InputStream pArg6, Iterable<ReaderInterceptor> pArg7, boolean pArg8) throws WebApplicationException, IOException {
        return null;
      }
      
      @Override
      public List<WriterModel> getWritersModelsForType(Class<?> pArg0) {
        return null;
      }
      
      @SuppressWarnings("rawtypes")
      @Override
      public Map<MediaType, List<MessageBodyWriter>> getWriters(MediaType pArg0) {
        return null;
      }
      
      @SuppressWarnings("rawtypes")
      @Override
      public Map<MediaType, List<MessageBodyReader>> getReaders(MediaType pArg0) {
        return null;
      }
      
      @Override
      public List<ReaderModel> getReaderModelsForType(Class<?> pArg0) {
        return null;
      }
      
      @SuppressWarnings("rawtypes")
      @Override
      public List<MessageBodyWriter> getMessageBodyWritersForType(Class<?> pArg0) {
        return null;
      }
      
      @Override
      public List<MediaType> getMessageBodyWriterMediaTypesByType(Class<?> pArg0) {
        return null;
      }
      
      @Override
      public List<MediaType> getMessageBodyWriterMediaTypes(Class<?> pArg0, Type pArg1, Annotation[] pArg2) {
        return null;
      }
      
      @Override
      public MediaType getMessageBodyWriterMediaType(Class<?> pArg0, Type pArg1, Annotation[] pArg2, List<MediaType> pArg3) {
        return null;
      }
      
      @Override
      public <T> MessageBodyWriter<T> getMessageBodyWriter(Class<T> pArg0, Type pArg1, Annotation[] pArg2, MediaType pArg3, PropertiesDelegate pArg4) {
        return null;
      }
      
      @Override
      public <T> MessageBodyWriter<T> getMessageBodyWriter(Class<T> pArg0, Type pArg1, Annotation[] pArg2, MediaType pArg3) {
        return null;
      }
      
      @SuppressWarnings("rawtypes")
      @Override
      public List<MessageBodyReader> getMessageBodyReadersForType(Class<?> pArg0) {
        return null;
      }
      
      @Override
      public List<MediaType> getMessageBodyReaderMediaTypesByType(Class<?> pArg0) {
        return null;
      }
      
      @Override
      public List<MediaType> getMessageBodyReaderMediaTypes(Class<?> pArg0, Type pArg1, Annotation[] pArg2) {
        return null;
      }
      
      @Override
      public <T> MessageBodyReader<T> getMessageBodyReader(Class<T> pArg0, Type pArg1, Annotation[] pArg2, MediaType pArg3, PropertiesDelegate pArg4) {
        return new MessageBodyReader<T>() {

          @Override
          public boolean isReadable(Class<?> pType, Type pGenericType, Annotation[] pAnnotations, MediaType pMediaType) {
            return true;
          }

          @SuppressWarnings("unchecked")
          @Override
          public T readFrom(Class<T> pType, Type pGenericType, Annotation[] pAnnotations, MediaType pMediaType,
              MultivaluedMap<String, String> pHttpHeaders, InputStream pEntityStream) throws IOException, WebApplicationException {
            /*
             * ONLY THE RAW STREAM
             */
            return (T)pEntityStream;
          }
        };
      }
      
      @Override
      public <T> MessageBodyReader<T> getMessageBodyReader(Class<T> pArg0, Type pArg1, Annotation[] pArg2, MediaType pArg3) {
        return getMessageBodyReader(pArg0, pArg1, pArg2, pArg3, null);
      }
    };
  }
}
```

We can use it like this :

```java
FormDataBodyPart filePart = FormDataBodyPartBuilder.ofFilename("src/test/data/sample.zip").withContentId("attached-file").withContentType("application/zip").build();
```


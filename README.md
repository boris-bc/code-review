# Https client

- [https-client](#https-client)
  - [Introduction](#introduction)
  - [Pre-requisites](#pre-requisites)
  - [Getting Started](#getting-started)

## Introduction

This is a native java library aimed at the simplification of the setup of the HTTPS clients. It is developed with apache http Client version 4.5.11.

## Pre-requisites

1) Java SDK version 1.8.
2) Any external service to connect to via HTTPS
3) Property file which defines the keystore or truststore certificates.

### Getting Started

1) In order to use this library you can create your API(RestController in case of Spring API) communicating with other services.

2) Then add https-client as a dependency in your project. This library provides you the following interface:

```java
public class HttpsClient {
    public CloseableHttpClient getHttpsClientWithTrustStore();
    public CloseableHttpClient getHttpsClientWithTrustStore(BasicCookieStore cookieStore);
    public CloseableHttpClient getHttpsClientWithKeyStoreAndTrustStore();
}
```
3) In order to use https-client, you need to provide a property file to initialize ConfigProperties used 
in the token service which includes the path to your truststore and keystore files and their following 
configuration parameters:

```java
public class ConfigProperties {
    private String apimlHost;
    private String apimlPort;
    private String apimlBaseUrl;
    private String keyStoreType;
    private String keyStorePath;
    private String keyStorePassword;
    private String trustStoreType;
    private String trustStorePath;
    private String trustStorePassword;
}
```

4)'https-client' allows you to have following functionality in your application:

a) HTTPS based communication without certificate authentication
To get properly created CloseableHttpClient just call one of the following two methods. The first method sets up HTTPS client without cookies. The second also provides CookieStore

```java
CloseableHttpClient getHttpsClientWithTrustStore();
 ``` 

```java
CloseableHttpClient getHttpsClientWithTrustStore(BasicCookieStore cookieStore);
 ``` 

b) HTTPS based communication with authentication via certificate

This method will automatically use the truststore file to add a security layer which you have configured using ConfigProperties class. It will also set up keystore with valid keys to be provided to the called service. 

```java
CloseableHttpClient getHttpsClientWithKeyStoreAndTrustStore();
 ``` 
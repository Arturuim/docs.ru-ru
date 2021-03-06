---
title: "Задание пользовательского алгоритма шифрования | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d662a305-8e09-451d-9a59-b0f12b012f1d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Задание пользовательского алгоритма шифрования
WCF позволяет указывать пользовательский алгоритм шифрования для использования при шифровании данных или вычислении цифровых подписей.  Для этого выполните следующие действия.  
  
1.  Создайте производный класс от класса <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.  
  
2.  Регистрация алгоритма  
  
3.  Настройте привязку с классом, который является производным от класса <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.  
  
## Создание производного класса от класса SecurityAlgorithmSuite  
 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> является абстрактным базовым классом, позволяющим указывать алгоритм, используемый при выполнении различных операций, связанных с безопасностью.  Например, вычисление хэша для цифровой подписи или шифрование сообщения.  В следующем коде показано, как наследовать класс от класса <xref:System.ServiceModel.Security.SecurityAlgorithm>.  
  
```csharp  
public class MyCustomAlgorithmSuite : SecurityAlgorithmSuite  
    {  
        public override string DefaultAsymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaOaepKeyWrap; }  
        }  
  
        public override string DefaultAsymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaSha1Signature; }  
        }  
  
        public override string DefaultCanonicalizationAlgorithm  
        {  
            get { return SecurityAlgorithms.ExclusiveC14n; ; }  
        }  
  
        public override string DefaultDigestAlgorithm  
        {  
            get { return SecurityAlgorithms.MyCustomHashAlgorithm; }  
        }  
  
        public override string DefaultEncryptionAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override int DefaultEncryptionKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSignatureKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSymmetricKeyLength  
        {  
            get { return 128; }  
        }  
  
        public override string DefaultSymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override string DefaultSymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.HmacSha1Signature; }  
        }  
  
        public override bool IsAsymmetricKeyLengthSupported(int length)  
        {  
            return length >= 1024 && length <= 4096;  
        }  
  
        public override bool IsSymmetricKeyLengthSupported(int length)  
        {  
            return length >= 128 && length <= 256;  
        }  
    }  
  
```  
  
## Регистрация пользовательского алгоритма  
 Регистрацию можно выполнить в файле конфигурации или в императивном коде.  Регистрация пользовательского алгоритма выполняется путем создания сопоставления между классом, реализующим поставщик службы шифрования, и псевдонимом.  Затем псевдоним сопоставляется с URI, который используется при указании алгоритма в привязке службы WCF.  Следующий фрагмент конфигурации показывает, как зарегистрировать пользовательский алгоритм в конфигурации.  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
           <cryptoClasses>  
              <cryptoClass SHA256CSP="System.Security.Cryptography.SHA256CryptoServiceProvider, System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
           </cryptoClasses>  
           <nameEntry name="http://constoso.com/CustomAlgorithms/CustomHashAlgorithm"  
              class="SHA256CSP" />  
           </cryptoNameMapping>  
        </cryptographySettings>  
    </mscorlib>  
</configuration>  
  
```  
  
 Раздел, находящийся под элементом \<`cryptoClasses`\>, создает сопоставление между поставщиком SHA256CryptoServiceProvider и псевдонимом «SHA256CSP».  Элемент \<[nameEntry](assetId:///nameEntry?qualifyHint=False&amp;autoUpgrade=True)\> создает сопоставление между псевдонимом «SHA256CSP» и указанным URL\-адресом \(http:\/\/constoso.com\/CustomAlgorithms\/CustomHashAlgorithm\).  
  
 Для регистрации пользовательского алгоритма в коде используйте метод [M:System.Security.Cryptography.CryptoConfig.AddAlgorithm\(System.Type, System.String\<xref:System.Security.Cryptography.CryptoConfig.AddAlgorithm%2A> System.String[])?qualifyHint=False&autoUpgrade=True.  Этот метод создает и оба сопоставления.  В следующем примере показано, как вызвать этот метод.  
  
```  
// Register the custom URI string defined for the hashAlgorithm in MyCustomAlgorithmSuite class to create the   
// SHA256CryptoServiceProvider hash algorithm object.  
CryptoConfig.AddAlgorithm(typeof(SHA256CryptoServiceProvider), "http://constoso.com/CustomAlgorithms/CustomHashAlgorithm");  
  
```  
  
## Настройка привязки  
 Привязка настраивается путем указания пользовательского класса, являющегося производным от класса <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>, в параметрах привязки, как показано в следующем фрагменте кода.  
  
```csharp  
WSHttpBinding binding = new WSHttpBinding();  
            binding.Security.Message.AlgorithmSuite = new MyCustomAlgorithmSuite();  
  
```  
  
 Полный пример кода приведен в образце [Криптографическая гибкость в системе безопасности WCF](../../../../docs/framework/wcf/samples/cryptographic-agility-in-wcf-security.md).  
  
## См. также  
 [Защита служб и клиентов](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Защита служб](../../../../docs/framework/wcf/securing-services.md)   
 [Общие сведения о безопасности](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Основные понятия безопасности](../../../../docs/framework/wcf/feature-details/security-concepts.md)
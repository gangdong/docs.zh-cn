---
title: 如何：创建使用自定义证书验证程序的服务
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, authentication
ms.assetid: bb0190ff-0738-4e54-8d22-c97d343708bf
ms.openlocfilehash: af1bb9b2ff793f6e6854c1b253dd445a35a5076f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185573"
---
# <a name="how-to-create-a-service-that-employs-a-custom-certificate-validator"></a>如何：创建使用自定义证书验证程序的服务
本主题介绍如何实现自定义证书验证程序，以及如何配置客户端或服务凭据以使用自定义证书验证程序替换默认证书验证逻辑。  
  
 如果 X.509 证书用于验证客户端或服务，则默认情况下 Windows 通信基础 （WCF） 使用 Windows 证书存储和加密 API 来验证该证书并确保它受信任。 有时，内置证书验证功能并不足够且必须更改。 WCF 通过允许用户添加自定义证书验证器，提供了一种更改验证逻辑的简单方法。 如果指定了自定义证书验证器，则 WCF 不使用内置证书验证逻辑，而是依赖于自定义验证器。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-create-a-custom-certificate-validator"></a>创建自定义证书验证程序  
  
1. 定义一个从 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 派生的新类。  
  
2. 实现抽象 <xref:System.IdentityModel.Selectors.X509CertificateValidator.Validate%2A> 方法。 将必须验证的证书作为自变量传递给该方法。 如果根据验证逻辑，传递的证书无效，则此方法引发 <xref:System.IdentityModel.Tokens.SecurityTokenValidationException>。 如果证书有效，则此方法返回到调用方。  
  
    > [!NOTE]
    > 若要将身份验证错误返回到客户端，应在 <xref:System.ServiceModel.FaultException> 方法中引发 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>。  
  
 [!code-csharp[c_CustomCertificateValidator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#2)]
 [!code-vb[c_CustomCertificateValidator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#2)]  
  
#### <a name="to-specify-a-custom-certificate-validator-in-service-configuration"></a>指定服务配置中的自定义证书验证程序  
  
1. 向[\<](../../configure-apps/file-schema/wcf/behaviors.md)[\<](../../configure-apps/file-schema/wcf/servicebehaviors.md)[系统\<](../../configure-apps/file-schema/wcf/system-servicemodel.md)添加>元素和服务行为>>。  
  
2. >添加[\<行为](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)并将`name`属性设置为适当的值。  
  
3. 将[\<服务凭据>](../../configure-apps/file-schema/wcf/servicecredentials.md)添加到`<behavior>`元素。  
  
4. 向 `<clientCertificate>` 元素中添加一个 `<serviceCredentials>` 元素。  
  
5. 向`<clientCertificate>`元素添加[\<身份验证>。](../../configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)  
  
6. 将 `customCertificateValidatorType` 属性设置为验证程序类型。 下面的示例将该属性设置为类型的命名空间和名称。  
  
7. 将 `certificateValidationMode` 属性设置为 `Custom`。  
  
    ```xml  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
       <serviceBehaviors>  
        <behavior name="ServiceBehavior">  
         <serviceCredentials>  
          <clientCertificate>  
          <authentication certificateValidationMode="Custom" customCertificateValidatorType="Samples.MyValidator, service" />  
          </clientCertificate>  
         </serviceCredentials>  
        </behavior>  
       </serviceBehaviors>  
      </behaviors>  
    </system.serviceModel>  
    </configuration>  
    ```  
  
#### <a name="to-specify-a-custom-certificate-validator-using-configuration-on-the-client"></a>使用客户端上的配置指定自定义证书验证程序  
  
1. 向[\<](../../configure-apps/file-schema/wcf/behaviors.md)[\<](../../configure-apps/file-schema/wcf/servicebehaviors.md)[系统\<](../../configure-apps/file-schema/wcf/system-servicemodel.md)添加>元素和服务行为>>。  
  
2. 添加[\<终结点行为>](../../configure-apps/file-schema/wcf/endpointbehaviors.md)元素。  
  
3. 添加一个 `<behavior>` 元素，并将 `name` 属性设置为适当的值。  
  
4. 添加[\<客户端凭据>](../../configure-apps/file-schema/wcf/clientcredentials.md)元素。  
  
5. >[\<添加服务证书](../../configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md)。  
  
6. 添加[\<身份验证>](../../configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)如以下示例所示。  
  
7. 将 `customCertificateValidatorType` 属性设置为验证程序类型。  
  
8. 将 `certificateValidationMode` 属性设置为 `Custom`。 下面的示例将该属性设置为类型的命名空间和名称。  
  
    ```xml  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
       <endpointBehaviors>  
        <behavior name="clientBehavior">  
         <clientCredentials>  
          <serviceCertificate>  
           <authentication certificateValidationMode="Custom"
                  customCertificateValidatorType=  
             "Samples.CustomX509CertificateValidator, client"/>  
          </serviceCertificate>  
         </clientCredentials>  
        </behavior>  
       </endpointBehaviors>  
      </behaviors>  
     </system.serviceModel>  
    </configuration>  
    ```  
  
#### <a name="to-specify-a-custom-certificate-validator-using-code-on-the-service"></a>使用服务上的代码指定自定义证书验证程序  
  
1. 指定 <xref:System.ServiceModel.Description.ServiceCredentials.ClientCertificate%2A> 属性的自定义证书验证程序。 您可以使用 <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> 属性访问服务凭据。  
  
2. 将 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A> 属性设置为 <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom>。  
  
 [!code-csharp[c_CustomCertificateValidator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#1)]
 [!code-vb[c_CustomCertificateValidator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#1)]  
  
#### <a name="to-specify-a-custom-certificate-validator-using-code-on-the-client"></a>使用客户端上的代码指定自定义证书验证程序  
  
1. 使用 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CustomCertificateValidator%2A> 属性指定自定义证书验证程序。 您可以使用 <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> 属性访问客户端凭据。 （由[ServiceModel 元数据实用程序工具 （Svcutil.exe）](../servicemodel-metadata-utility-tool-svcutil-exe.md)生成的客户端类始终派生<xref:System.ServiceModel.ClientBase%601>自该类。  
  
2. 将 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> 属性设置为 <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom>。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 下面的示例演示自定义证书验证程序的实现及其在服务上的用法。  
  
### <a name="code"></a>代码  
 [!code-csharp[c_CustomCertificateValidator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#3)]
 [!code-vb[c_CustomCertificateValidator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#3)]  
  
## <a name="see-also"></a>另请参阅

- <xref:System.IdentityModel.Selectors.X509CertificateValidator>

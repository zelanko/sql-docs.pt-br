---
title: Usar criptografia | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f769e35477d564365df702bd768ac1953c7affa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "71712969"
---
# <a name="using-encryption"></a>Usando criptografia

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A criptografia do protocolo TLS permite a transmissão de dados criptografados pela rede entre uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um aplicativo cliente.  
  
O protocolo TLS é um protocolo que estabelece um canal de comunicação seguro para impedir a intercepção de informações críticas ou confidenciais pela rede e outras comunicações de Internet. O TLS permite o cliente e o servidor autentiquem a identidade um do outro. Depois que os participantes são autenticados, o TLS fornece conexões criptografadas entre eles para transmissão de mensagem segura.  
  
O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece uma infraestrutura para habilitar e desabilitar a criptografia em uma conexão específica com base nas propriedades de conexão do usuário especificado e nas configurações de servidor e cliente. O usuário pode especificar o local de repositório de certificados e senha, um nome de host a ser usado para validar o certificado, e quando criptografar o canal de comunicação.  
  
A habilitação da criptografia TLS aumenta a segurança dos dados transmitidos pelas redes entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos. Porém, a habilitação da criptografia reduz o desempenho.  
  
Os tópicos nesta seção descrevem como a versão [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte à criptografia TLS, incluindo novas propriedades de conexão, e como você pode configurar o repositório de confiança no lado do cliente.  
  
> [!NOTE]  
> A propriedade de conexão **hostNameInCertificate** é recomendada para validar um certificado TLS.  

## <a name="in-this-section"></a>Nesta seção  

| Tópico                                                                                                        | Descrição                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Noções básicas sobre suporte à criptografia](../../connect/jdbc/understanding-ssl-support.md)                                 | Descreve como o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte à criptografia TLS.                                              |
| [Conectando-se com criptografia](../../connect/jdbc/connecting-with-ssl-encryption.md)                       | Descreve como conectar-se a um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as novas propriedades de conexão específicas do TLS. |
| [Configurando o cliente para criptografia](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md) | Descreve como configurar o repositório de confiança padrão do lado do cliente e como importar um certificado privado para o repositório de confiança do computador cliente.   |
  
## <a name="see-also"></a>Confira também

[Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  

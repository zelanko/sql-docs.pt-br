---
title: Seção conexão do arquivo de personalização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1de3710590cf49de30ff8e79a6ff829b124c42dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922803"
---
# <a name="customization-file-connect-section"></a>Seção Conexão do arquivo de personalização
O comportamento padrão do manipulador é negar todas as conexões. O **conectar** seção especifica as exceções a esse comportamento. Por exemplo, se todos os **conectar** seções foram ausente ou vazio e, em seguida, por padrão não foi possível estabelecer conexões.  
  
 O **conectar** seção pode conter:  
  
-   Uma entrada de acesso padrão que especifica o padrão ler e gravar operações permitidas nesta conexão. Se não houver nenhuma entrada de acesso padrão na seção, a seção será ignorada.  
  
-   Uma nova cadeia de conexão que substitui a cadeia de caracteres de conexão do cliente.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 É uma entrada de acesso padrão do formulário:  
  
```console
  
Access=  
accessRight  
  
```  
  
 É uma entrada de cadeia de caracteres de conexão de substituição do formulário:  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Comentários  
  
|Parte|Descrição|  
|----------|-----------------|  
|**Connect**|Uma cadeia de caracteres literal que indica que essa é uma entrada de cadeia de caracteres de conexão.|  
|**_connectionString_**|Uma cadeia de caracteres que substitui a cadeia de caracteres de conexão de cliente inteira.|  
|**Acesso**|Uma cadeia de caracteres literal que indica que essa é uma entrada de acesso.|  
|**_accessRight_**|Um dos seguintes direitos de acesso:<br /><br /> -   **NoAccess** -usuário não pode acessar a fonte de dados.<br />-   **ReadOnly** -o usuário pode ler a fonte de dados.<br />-   **ReadWrite** -usuário pode ler ou gravar na fonte de dados.|  
  
 Se você quiser permitir qualquer conexão (em vigor, desabilitando o comportamento do manipulador padrão), defina a entrada de acesso **conexão padrão** seção `Access=ReadWrite`e exclua ou comente a qualquer outro **conectar** _identificador_ seção.  
  
## <a name="see-also"></a>Consulte também  
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção de UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)




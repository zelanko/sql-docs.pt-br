---
title: Arquivo de personalização de conectar-se a seção | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc00af717ef3161f414525f109236b0aba0c442e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="customization-file-connect-section"></a>Arquivo de personalização de conectar-se a seção
O comportamento padrão do manipulador é negar todas as conexões. O **conectar** seção especifica exceções a esse comportamento. Por exemplo, se todos os **conectar** seções foram ausente ou vazia, em seguida, por padrão não foi possível estabelecer conexões.  
  
 O **conectar** seção pode conter:  
  
-   Uma entrada de acesso padrão que especifica o padrão ler e gravar operações permitidas nesta conexão. Se não houver nenhuma entrada de acesso padrão na seção, a seção será ignorada.  
  
-   Uma nova cadeia de conexão que substitui a cadeia de caracteres de conexão do cliente.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 É uma entrada de acesso padrão do formulário:  
  
```  
  
Access=  
accessRight  
  
```  
  
 É uma entrada de cadeia de caracteres de conexão de substituição do formulário:  
  
```  
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Remarks  
  
|Parte|Description|  
|----------|-----------------|  
|**Conectar**|Uma cadeia de caracteres literal que indica que isso é uma entrada de cadeia de caracteres de conexão.|  
|***connectionString***|Uma cadeia de caracteres que substitui a cadeia de caracteres de conexão de cliente inteira.|  
|**Acesso**|Uma cadeia de caracteres literal que indica que isso é uma entrada de acesso.|  
|***accessRight***|Um dos seguintes direitos de acesso:<br /><br /> -   **NoAccess** — usuário não pode acessar a fonte de dados.<br />-   **ReadOnly** — o usuário pode ler a fonte de dados.<br />-   **ReadWrite** — usuário pode ler ou gravar para a fonte de dados.|  
  
 Se você deseja permitir qualquer conexão (em vigor, desabilitando o comportamento de manipulador padrão), defina a entrada de acesso **conexão padrão** seção `Access=ReadWrite`e exclua ou comente a qualquer outro **conectar** *identificador* seção.  
  
## <a name="see-also"></a>Consulte também  
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção do arquivo UserList de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)




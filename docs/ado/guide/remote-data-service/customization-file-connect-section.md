---
title: Seção conexão de arquivo de personalização | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922803"
---
# <a name="customization-file-connect-section"></a>Seção Conexão do arquivo de personalização
O comportamento padrão do manipulador é negar todas as conexões. A seção **conectar** especifica exceções para esse comportamento. Por exemplo, se todas as seções de **conexão** estiverem ausentes ou vazias, por padrão, nenhuma conexão poderá ser feita.  
  
 A seção **conectar** pode conter:  
  
-   Uma entrada de acesso padrão que especifica as operações de leitura e gravação padrão permitidas nesta conexão. Se não houver nenhuma entrada de acesso padrão na seção, a seção será ignorada.  
  
-   Uma nova cadeia de conexão que substitui a cadeia de conexão do cliente.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 Uma entrada de acesso padrão está no formato:  
  
```console
  
Access=  
accessRight  
  
```  
  
 Uma entrada de cadeia de conexão de substituição está no formato:  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Comentários  
  
|Parte|DESCRIÇÃO|  
|----------|-----------------|  
|**Connect**|Uma cadeia de caracteres literal que indica que se trata de uma entrada de cadeia de conexão.|  
|**_connectionString_**|Uma cadeia de caracteres que substitui toda a cadeia de conexão do cliente.|  
|**Access**|Uma cadeia de caracteres literal que indica que se trata de uma entrada de acesso.|  
|**_accessRight_**|Um dos seguintes direitos de acesso:<br /><br /> -   **NoAccess** -o usuário não pode acessar a fonte de dados.<br />-   **ReadOnly** -o usuário pode ler a fonte de dados.<br />-   **ReadWrite** -o usuário pode ler ou gravar na fonte de dados.|  
  
 Se você quiser permitir qualquer conexão (na verdade, desabilitando o comportamento do manipulador padrão), defina a entrada de acesso na seção **conectar padrão** como `Access=ReadWrite`e exclua ou comente qualquer outra seção do _identificador_ de **conexão** .  
  
## <a name="see-also"></a>Consulte Também  
 [Seção de logs de arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização de datafactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações do cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrever seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)




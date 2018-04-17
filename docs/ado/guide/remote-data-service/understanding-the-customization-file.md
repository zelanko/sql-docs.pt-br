---
title: Noções básicas sobre o arquivo de personalização | Microsoft Docs
ms.prod: sql-non-specified
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
ms.topic: article
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0597c403a9d716c155fe129ab8cb514268b27341
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2018
---
# <a name="understanding-the-customization-file"></a>Noções básicas sobre o arquivo de personalização
Cada cabeçalho de seção no arquivo de personalização consiste em colchetes (**[]**) que contém um tipo e o parâmetro. Os tipos de quatro seção são indicados por cadeias de caracteres literais **conectar**, **sql**, **userlist**, ou **logs**. O parâmetro é a cadeia de caracteres literal, o padrão, um identificador de usuário especificado ou nada.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Portanto, cada seção está marcada com um dos cabeçalhos da seção a seguir:  
  
```  
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 Os cabeçalhos de seção tem as seguintes partes.  
  
|Parte|Description|  
|----------|-----------------|  
|**connect**|Uma cadeia de caracteres literal que modifica uma cadeia de caracteres de conexão.|  
|**sql**|Uma cadeia de caracteres literal que modifica uma cadeia de caracteres de comando.|  
|**userlist**|Uma cadeia de caracteres literal que modifica os direitos de acesso de um usuário específico.|  
|**logs**|Uma cadeia de caracteres literal que especifica um arquivo de log operacionais erros de gravação.|  
|**default**|Uma cadeia de caracteres literal que será usada se nenhum identificador é especificada ou encontrada.|  
|*identifier*|Uma cadeia de caracteres que corresponde a uma cadeia de caracteres de **conectar** ou **comando** cadeia de caracteres.<br /><br /> -Use esta seção se o cabeçalho de seção contém **conectar** e a cadeia de caracteres do identificador foi encontrada na cadeia de conexão.<br />-Use esta seção se o cabeçalho de seção contém **sql** e a cadeia de caracteres do identificador foi encontrada na cadeia de caracteres de comando.<br />-Use esta seção se o cabeçalho de seção contém **userlist** e a cadeia de caracteres do identificador corresponde uma **conectar** identificador de seção.|  
  
 O **DataFactory** chama o manipulador, passando parâmetros de cliente. O manipulador de pesquisa para cadeias de caracteres inteiras nos parâmetros do cliente que correspondem a identificadores nos cabeçalhos de seção apropriada. Se uma correspondência for encontrada, o conteúdo dessa seção é aplicado para o parâmetro do cliente.  
  
 Uma seção específica é usada nas seguintes circunstâncias:  
  
-   Um **conectar-se** seção é usada se a parte do valor do cliente se conectar a palavra-chave de cadeia de caracteres, "**fonte de dados = * valor*", corresponde a um **conectar** identificador de seção*.*  
  
-   Um **sql** seção será usada se a cadeia de caracteres de comando do cliente contém uma cadeia de caracteres que corresponde a um **sql** identificador de seção.  
  
-   Um **conectar** ou **sql** seção com um parâmetro padrão é usada se não houver nenhum identificador correspondente.  
  
-   Um **userlist** seção será usada se o **userlist** seção correspondências de identificador um **conectar** identificador de seção. Se houver uma correspondência, o conteúdo do **userlist** seção são aplicadas para a conexão controlado pelo **conectar** seção.  
  
-   Se a cadeia de caracteres em uma cadeia de conexão ou o comando não coincide com o identificador em qualquer **conectar** ou **sql** cabeçalho da seção e não há nenhum **conectar** ou **sql**  seção cabeçalho com um parâmetro padrão, em seguida, a cadeia de caracteres do cliente é usada sem modificação.  
  
-   O **logs** seção é usada sempre que o **DataFactory** está em operação.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de personalização de conectar-se a seção](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção do arquivo UserList de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)





















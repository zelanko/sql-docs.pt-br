---
title: Noções básicas sobre o arquivo de personalização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31d486f24d9c06926462be856d9102a9a457bb7b
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558713"
---
# <a name="understanding-the-customization-file"></a>Noções básicas sobre o arquivo de personalização
Cada cabeçalho de seção no arquivo de personalização é formado por colchetes (**[]**) que contém um tipo e o parâmetro. Os tipos de quatro seção são indicados por cadeias de caracteres literais **conectar-se**, **sql**, **userlist**, ou **logs**. O parâmetro é a cadeia de caracteres literal, o padrão, um identificador especificado pelo usuário ou nada.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Portanto, cada seção é marcada com um dos cabeçalhos de seção a seguir:  
  
```console
  
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
|**default**|Uma cadeia de caracteres literal que será usada se nenhum identificador é especificado ou localizado.|  
|*identifier*|Uma cadeia de caracteres que corresponde a uma cadeia de caracteres a **conectar-se** ou **comando** cadeia de caracteres.<br /><br /> -Use esta seção se o cabeçalho de seção contém **conectar-se** e a cadeia de caracteres de identificador for encontrada na cadeia de conexão.<br />-Use esta seção se o cabeçalho de seção contém **sql** e a cadeia de caracteres de identificador for encontrada na cadeia de caracteres de comando.<br />-Use esta seção se o cabeçalho de seção contém **userlist** e a cadeia de caracteres de identificador corresponde uma **conectar** identificador de seção.|  
  
 O **DataFactory** chama o manipulador, passando parâmetros de cliente. O manipulador de procura cadeias de caracteres inteiras nos parâmetros de cliente que correspondem aos identificadores nos cabeçalhos de seção apropriada. Se uma correspondência for encontrada, o conteúdo dessa seção é aplicado para o parâmetro do cliente.  
  
 Uma seção específica é usada nas seguintes circunstâncias:  
  
-   Um **conectar-se** seção é usada se a parte do valor do cliente se conectar a palavra-chave de cadeia de caracteres, "**fonte de dados = * * * valor*", corresponde a um **conectar** identificador de seção *.*  
  
-   Uma **sql** seção será usada se a cadeia de caracteres de comando do cliente contém uma cadeia de caracteres que corresponde a um **sql** identificador de seção.  
  
-   Um **conectar-se** ou **sql** seção com um parâmetro padrão é usada se não houver nenhum identificador correspondente.  
  
-   Um **userlist** seção será usada se o **userlist** correspondências de identificador de seção um **conectar** identificador de seção. Se houver uma correspondência, o conteúdo do **userlist** seção são aplicadas para a conexão regulado a **conectar-se** seção.  
  
-   Se a cadeia de caracteres em uma cadeia de conexão ou o comando não coincide com o identificador em qualquer **conectar-se** ou **sql** cabeçalho da seção e não há nenhum **conectar** ou **sql**  seção de cabeçalho com um parâmetro padrão, em seguida, a cadeia de caracteres do cliente for usada sem modificação.  
  
-   O **logs** seção é usada sempre que o **DataFactory** está em operação.  
  
## <a name="see-also"></a>Consulte também  
 [Seção conexão do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção de UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


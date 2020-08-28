---
description: Noções básicas sobre o arquivo de personalização
title: Noções básicas sobre o arquivo de personalização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: rothja
ms.author: jroth
ms.openlocfilehash: 9b097d54015d9f48140aafb6feb360b8013edeaf
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977387"
---
# <a name="understanding-the-customization-file"></a>Noções básicas sobre o arquivo de personalização
Cada cabeçalho de seção no arquivo de personalização consiste em colchetes (**[]**) contendo um tipo e um parâmetro. Os quatro tipos de seção são indicados pelas cadeias de caracteres literais **Connect**, **SQL**, **UserList**ou **logs**. O parâmetro é a cadeia de caracteres literal, o padrão, um identificador especificado pelo usuário ou nada.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Portanto, cada seção é marcada com um dos seguintes cabeçalhos de seção:  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 Os cabeçalhos de seção têm as seguintes partes.  
  
|Parte|Descrição|  
|----------|-----------------|  
|**connect**|Uma cadeia de caracteres literal que modifica uma cadeia de conexão.|  
|**SQL**|Uma cadeia de caracteres literal que modifica uma cadeia de caracteres de comando.|  
|**UserList**|Uma cadeia de caracteres literal que modifica os direitos de acesso de um usuário específico.|  
|**logs**|Uma cadeia de caracteres literal que especifica um arquivo de log que registra erros operacionais.|  
|**default**|Uma cadeia de caracteres literal que será usada se nenhum identificador for especificado ou encontrado.|  
|*ID*|Uma cadeia de caracteres que corresponde a uma cadeia de caracteres na cadeia de caracteres de **conexão** ou de **comando** .<br /><br /> -Use esta seção se o cabeçalho da seção contiver **Connect** e a cadeia de caracteres do identificador for encontrada na cadeia de conexão.<br />-Use esta seção se o cabeçalho da seção contiver **SQL** e a cadeia de caracteres do identificador for encontrada na cadeia de caracteres de comando.<br />-Use esta seção se o cabeçalho da seção contiver **UserList** e a cadeia de caracteres do identificador corresponder a um identificador de seção de **conexão** .|  
  
 O **DataFactory** chama o manipulador, passando parâmetros do cliente. O manipulador procura cadeias de caracteres inteiras nos parâmetros do cliente que correspondem aos identificadores nos cabeçalhos de seção apropriados. Se uma correspondência for encontrada, o conteúdo dessa seção será aplicado ao parâmetro do cliente.  
  
 Uma seção específica é usada nas seguintes circunstâncias:  
  
-   Uma seção de **conexão** é usada se a parte de valor da palavra-chave String de conexão do cliente, "**Data Source =**_Value_", corresponde a um identificador de seção de **conexão** . 
  
-   Uma seção **SQL** será usada se a cadeia de caracteres de comando do cliente contiver uma cadeia de caracteres que corresponda a um identificador de seção **SQL** .  
  
-   Uma seção **Connect** ou **SQL** com um parâmetro padrão será usada se não houver nenhum identificador correspondente.  
  
-   Uma seção **UserList** será usada se o identificador da seção **UserList** corresponder a um identificador de seção de **conexão** . Se houver uma correspondência, o conteúdo da seção **UserList** será aplicado à conexão governada pela seção **Connect** .  
  
-   Se a cadeia de caracteres em uma conexão ou cadeia de caracteres de comando não corresponder ao identificador em nenhum cabeçalho de seção **Connect** ou **SQL** e não houver nenhum cabeçalho de **conexão** ou de seção **SQL** com um parâmetro padrão, a cadeia de caracteres do cliente será usada sem modificação.  
  
-   A seção **logs** é usada sempre que o **DataFactory** estiver em operação.  
  
## <a name="see-also"></a>Consulte Também  
 [Seção conexão de arquivo de personalização](./customization-file-connect-section.md)   
 [Seção de logs de arquivo de personalização](./customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](./customization-file-sql-section.md)   
 [Seção UserList do arquivo de personalização](./customization-file-userlist-section.md)   
 [Personalização de datafactory](./datafactory-customization.md)   
 [Configurações do cliente necessárias](./required-client-settings.md)   
 [Escrever seu próprio manipulador personalizado](./writing-your-own-customized-handler.md)
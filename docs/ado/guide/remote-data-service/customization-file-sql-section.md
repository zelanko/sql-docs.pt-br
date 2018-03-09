---
title: "Seção SQL do arquivo de personalização | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06b3a79e97c50df8c7eed17b1343030ca2280426
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="customization-file-sql-section"></a>Seção SQL do arquivo de personalização
O **sql** seção pode conter uma nova cadeia de caracteres SQL que substitui a cadeia de caracteres de comando do cliente. Se não houver nenhuma cadeia de caracteres SQL da seção, a seção será ignorada.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 A nova cadeia de caracteres SQL pode ser *parametrizadas*. Ou seja, os parâmetros no **sql** seção cadeia de caracteres SQL (designado pelo '?' caracteres) podem ser substituídos por argumentos correspondentes em um *identificador* na cadeia de caracteres de comando do cliente (designado por um lista delimitada por parênteses). O identificador e uma lista de argumentos se comportam como uma chamada de função.  
  
 Por exemplo, suponha que a cadeia de caracteres de comando do cliente é `"CustomerByID(4)"`, o cabeçalho de seção do SQL é `[SQL CustomerByID]`, e a nova cadeia de caracteres de seção SQL é `"SELECT * FROM Customers WHERE CustomerID = ?".` irá gerar o manipulador `"SELECT * FROM Customers WHERE CustomerID = 4"` e usar essa cadeia de caracteres para consultar a fonte de dados.  
  
 Se a nova instrução SQL é a cadeia de caracteres nula (""), a seção será ignorada.  
  
 Se a nova cadeia de instrução SQL não é válida, a execução da instrução falhará. O parâmetro do cliente é ignorado. Você pode fazer isso intencionalmente para "Desativar" todos os comandos SQL do cliente, especificando:  
  
```  
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Sintaxe  
 É uma entrada de cadeia de caracteres SQL da substituição do formulário:  
  
 **SQL=**   
 ***sqlString***  
  
|Parte|Description|  
|----------|-----------------|  
|**SQL**|Uma cadeia de caracteres literal que indica que isso é uma entrada de seção do SQL.|  
|***sqlString***|Uma cadeia de caracteres SQL que substitui a cadeia de caracteres do cliente.|  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de personalização de conectar-se a seção](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção do arquivo UserList de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



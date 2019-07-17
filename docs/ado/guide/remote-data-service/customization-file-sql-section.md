---
title: Seção SQL do arquivo de personalização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6163a5b5fd0999e17e17961639e0a1fee3e8fa4c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922795"
---
# <a name="customization-file-sql-section"></a>Seção SQL do arquivo de personalização
O **sql** seção pode conter uma nova cadeia de caracteres SQL que substitui a cadeia de caracteres de comando do cliente. Se não houver nenhuma cadeia de caracteres SQL na seção, a seção será ignorada.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Nova cadeia de caracteres SQL pode ser *parametrizada*. Ou seja, os parâmetros na **sql** seção da cadeia de caracteres SQL (designado pelo '?' caractere) podem ser substituídos pelos argumentos correspondentes em um *identificador* na cadeia de caracteres de comando do cliente (designado por um lista delimitada por parênteses). O identificador e a lista de argumentos se comportam como uma chamada de função.  
  
 Por exemplo, suponha que a cadeia de caracteres de comando do cliente é `"CustomerByID(4)"`, o cabeçalho de seção SQL é `[SQL CustomerByID]`, e a nova cadeia de caracteres de seção SQL é `"SELECT * FROM Customers WHERE CustomerID = ?".` gerará o manipulador `"SELECT * FROM Customers WHERE CustomerID = 4"` e usar essa cadeia de caracteres para consultar a fonte de dados.  
  
 Se a nova instrução SQL é a cadeia de caracteres nula (""), a seção será ignorada.  
  
 Se a nova cadeia de caracteres de instrução de SQL não for válida, a execução da instrução falhará. O parâmetro do cliente é ignorado. Você pode fazer isso intencionalmente para "desligar" todos os comandos SQL de cliente, especificando:  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Sintaxe  
 É uma substituição de entrada de cadeia de caracteres SQL da forma:  
  
 **SQL=**    
 ***sqlString***  
  
|Parte|Descrição|  
|----------|-----------------|  
|**SQL**|Uma cadeia de caracteres literal que indica que essa é uma entrada de seção SQL.|  
|***sqlString***|Uma cadeia de caracteres SQL que substitui a cadeia de caracteres do cliente.|  
  
## <a name="see-also"></a>Consulte também  
 [Seção conexão do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção de UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



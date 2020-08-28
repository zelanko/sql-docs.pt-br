---
description: Seção SQL do arquivo de personalização
title: Seção SQL do arquivo de personalização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: rothja
ms.author: jroth
ms.openlocfilehash: 210363a1a852aa3c059c7929af1c07a9fe32c6ae
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978227"
---
# <a name="customization-file-sql-section"></a>Seção SQL do arquivo de personalização
A seção **SQL** pode conter uma nova cadeia de caracteres SQL que substitui a cadeia de caracteres de comando do cliente. Se não houver nenhuma cadeia de caracteres SQL na seção, a seção será ignorada.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 A nova cadeia de caracteres SQL pode ser *parametrizada*. Ou seja, os parâmetros na cadeia de caracteres SQL da seção **SQL** (designado pelo caractere '? ') podem ser substituídos por argumentos correspondentes em um *identificador* na cadeia de caracteres de comando do cliente (designado por uma lista delimitada por vírgula entre parênteses). O identificador e a lista de argumentos se comportam como uma chamada de função.  
  
 Por exemplo, suponha que a cadeia de caracteres de comando do cliente seja `"CustomerByID(4)"` , o cabeçalho da seção SQL seja `[SQL CustomerByID]` , e a nova cadeia de caracteres da seção SQL seja `"SELECT * FROM Customers WHERE CustomerID = ?".` o manipulador irá gerar `"SELECT * FROM Customers WHERE CustomerID = 4"` e usar essa cadeia de caracteres para consultar a fonte de dados.  
  
 Se a nova instrução SQL for a cadeia de caracteres nula (""), a seção será ignorada.  
  
 Se a nova cadeia de caracteres de instrução SQL não for válida, a execução da instrução falhará. O parâmetro do cliente é efetivamente ignorado. Você pode fazer isso intencionalmente para "desativar" todos os comandos de cliente SQL especificando:  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Sintaxe  
 Uma entrada de cadeia de caracteres SQL substituta está no formato:  
  
 **SQL =**   
 ***sqlString***  
  
|Parte|Descrição|  
|----------|-----------------|  
|**SQL**|Uma cadeia de caracteres literal que indica que se trata de uma entrada de seção SQL.|  
|***sqlString***|Uma cadeia de caracteres SQL que substitui a cadeia de caracteres do cliente.|  
  
## <a name="see-also"></a>Consulte Também  
 [Seção conexão de arquivo de personalização](./customization-file-connect-section.md)   
 [Seção de logs de arquivo de personalização](./customization-file-logs-section.md)   
 [Seção UserList do arquivo de personalização](./customization-file-userlist-section.md)   
 [Personalização de datafactory](./datafactory-customization.md)   
 [Configurações do cliente necessárias](./required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](./understanding-the-customization-file.md)   
 [Escrever seu próprio manipulador personalizado](./writing-your-own-customized-handler.md)
---
title: "Criando uma cadeia de caracteres de Conexão | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 90105b448604f3b99fefc2598fa375677f0bbdb4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="creating-a-connection-string"></a>Criando uma cadeia de conexão
Uma cadeia de caracteres de conexão consiste em uma lista de pares de valor do argumento (isto é, parâmetros), separada por ponto e vírgula. Por exemplo:  
  
```  
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 Todos os parâmetros devem ser reconhecidos pelo ADO ou o provedor especificado.  
  
 ADO reconhece os seguintes cinco argumentos em uma cadeia de caracteres de conexão.  
  
|Argumento|Description|  
|--------------|-----------------|  
|*Provedor*|Especifica o nome de um provedor a ser usado para a conexão.|  
|*Nome do Arquivo*|Especifica o nome de um arquivo específico do provedor (por exemplo, um objeto de fonte de dados persistentes) que contém informações de conexão predefinidos.|  
|*URL*|Especifica a cadeia de caracteres de conexão como uma URL absoluta que identifica um recurso, como um arquivo ou diretório.|  
|*Provedor remoto*|Especifica o nome de um provedor a ser usada ao abrir uma conexão de cliente. (Apenas serviço de dados remotos.)|  
|*Servidor remoto*|Especifica o nome do caminho do servidor a ser usada ao abrir uma conexão de cliente. (Apenas serviço de dados remotos.)|  
  
 Outros argumentos são passados para o provedor chamado no *provedor* argumento, sem nenhum processamento pelo ADO.  
  
 O aplicativo HelloData em [HelloData: um simples aplicativo de ADO](../../../ado/guide/data/hellodata-a-simple-ado-application.md) usada a seguinte cadeia de conexão:  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 Nessa cadeia de caracteres de conexão, o ADO reconhece somente o `"Provider=SQLOLEDB"` parâmetro, que especifica o provedor OLE DB da Microsoft para SQL Server como a fonte de dados do ADO. O restante dos pares de valor do argumento, `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`, são passadas textual para esse provedor. O tipo e a validade desses parâmetros são específicos do provedor. Para obter informações sobre os parâmetros válidos que podem ser passados na cadeia de conexão, consulte a documentação do provedor individuais.  
  
 Acordo com o OLE DB Provider para obter a documentação do SQL Server, você pode substituir "Server" para o *fonte de dados* parâmetro e "Banco de dados" para o *catálogo inicial* parâmetro. Assim, a seguinte cadeia de conexão pode produzir resultados idênticos ao acima:  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```

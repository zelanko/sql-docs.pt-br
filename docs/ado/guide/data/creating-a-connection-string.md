---
description: Criando uma cadeia de conexão
title: Criando uma cadeia de conexão | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
author: rothja
ms.author: jroth
ms.openlocfilehash: 0fcd3b23a6aeaa86b33650acf677dc132e8219d1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991497"
---
# <a name="creating-a-connection-string"></a>Criando uma cadeia de conexão
Uma cadeia de conexão consiste em uma lista de pares de argumento/valor (ou seja, parâmetros), separados por ponto e vírgula. Por exemplo:  
  
```syntax
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 Todos os parâmetros devem ser reconhecidos pelo ADO ou pelo provedor especificado.  
  
 O ADO reconhece os cinco argumentos a seguir em uma cadeia de conexão.  
  
|Argumento|Descrição|  
|--------------|-----------------|  
|*Provedor*|Especifica o nome de um provedor a ser usado para a conexão.|  
|*Nome do Arquivo*|Especifica o nome de um arquivo específico do provedor (por exemplo, um objeto de fonte de dados persistente) que contém informações de conexão predefinidas.|  
|*URL*|Especifica a cadeia de conexão como uma URL absoluta que identifica um recurso, como um arquivo ou diretório.|  
|*Provedor remoto*|Especifica o nome de um provedor a ser usado ao abrir uma conexão do lado do cliente. (Somente serviço de dados remotos.)|  
|*Servidor remoto*|Especifica o nome do caminho do servidor a ser usado ao abrir uma conexão do lado do cliente. (Somente serviço de dados remotos.)|  
  
 Outros argumentos são passados para o provedor chamado no argumento do *provedor* , sem nenhum processamento pelo ADO.  
  
 O aplicativo HelloData em [HelloData: um aplicativo ADO simples](./hellodata-a-simple-ado-application.md) usou a seguinte cadeia de conexão:  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 Nessa cadeia de conexão, o ADO reconhece apenas o `"Provider=SQLOLEDB"` parâmetro, que especifica o provedor de OLE DB da Microsoft para SQL Server como a fonte de dados ADO. O restante dos pares de argumento/valor, `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"` , são passados literalmente para esse provedor. O tipo e a validade desses parâmetros são específicos do provedor. Para obter informações sobre parâmetros válidos que podem ser passados na cadeia de conexão, consulte a documentação do provedor individual.  
  
 De acordo com o provedor de OLE DB para SQL Server documentação, você pode substituir "Server" para o parâmetro de *fonte de dados* e "Database" para o parâmetro de *catálogo inicial* . Assim, a cadeia de conexão a seguir produziria resultados idênticos ao mostrado acima:  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
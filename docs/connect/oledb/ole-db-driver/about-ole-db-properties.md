---
title: Sobre as propriedades de conexão do OLE DB | Microsoft Docs
description: No Driver do OLE DB para SQL Server, os consumidores definem valores de propriedade para solicitar um comportamento de objeto específico. Saiba mais sobre como definir propriedades.
ms.custom: ''
ms.date: 05/20/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- OLE DB Driver for SQL Server, properties
- properties [OLE DB]
- property values [OLE DB Driver for SQL Server]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1cd1a9f56ff4ac70ee0802bed3ffc7856c04678e
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862342"
---
# <a name="about-ole-db-properties"></a>Sobre propriedades OLE DB
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

<!--
NOTE , GeneMi , 2020/May/20:
    This SQL 2016+ article is a nearly exact duplicate of another SQL 2016+ article.
    This article resides under docs/connect/oledb/ole-db-driver/.

    The other article resides under docs/relational-databases/native-client-ole-db-provider/.
    And, the other article has a SQL 2014 counterpart having its same GitHub directory path and filename, to support SQL 2014 OPS Versioning with SQL 2016+.

    This path-file name is:
'\sql-docs-pr\docs\connect\oledb\ole-db-driver\about-ole-db-properties.md'.

    The other path-file is named:
'\sql-docs-pr\docs\relational-databases\native-client-ole-db-provider\about-ole-db-properties.md'.

    Therefore, maybe this docs/connect/oledb/... file should be deleted?

1611957:  This NOTE relates to SEO content bug 1611957 about metadata 'title:' value duplication:
    https://mseng.visualstudio.com/TechnicalContent/_workitems/edit/1611957

PR 15068:  This HTML comment is being added by PR...
    https://github.com/MicrosoftDocs/sql-docs-pr/pull/15068
-->

  Os consumidores definem valores de propriedade para solicitar um comportamento de objeto específico. Por exemplo, os consumidores usam propriedades para especificar as interfaces a serem expostas por um conjunto de linhas. Eles obtêm os valores de propriedade para determinar os recursos de um objeto, como um conjunto de linhas, uma sessão ou um objeto de fonte de dados.  
  
 Cada propriedade tem um valor, um tipo, uma descrição e um atributo de leitura/gravação e, no caso de propriedades de conjunto de linhas, um indicador que determina se ela pode ser aplicada por coluna.  
  
 Uma propriedade é identificada por um GUID e um inteiro que representam a ID de propriedade. Um conjunto de propriedades é um conjunto de todas as propriedades que compartilham o mesmo GUID. Além dos conjuntos predefinidos de conjuntos de propriedades OLE DB, o OLE DB Driver for SQL Server implementa propriedades e conjuntos de propriedades específicos do provedor neles. Cada propriedade pertence a um ou mais grupos de propriedades. Um grupo de propriedades é o grupo de todas as propriedades que se aplicam a um objeto específico. Alguns grupos de propriedades incluem o grupo de propriedades de inicialização, o grupo de propriedades de fonte de dados, o grupo de propriedades de sessão, o grupo de propriedades de conjunto de linhas, o grupo de propriedades de tabela e o grupo de propriedades de coluna. Há propriedades em cada um desses grupos de propriedade.  
  
 A definição dos valores de propriedade envolve:  
  
1.  Determinar as propriedades para as quais definir valores.  
  
2.  Determinar os conjuntos de propriedades que contêm as propriedades identificadas.  
  
3.  Alocar uma matriz de estruturas DBPROPSET, uma para cada conjunto de propriedades identificadas.  
  
4.  Alocar uma matriz de estruturas DBPROP para cada conjunto de propriedades. O número de elementos em cada matriz é o número de propriedades (identificadas na Etapa 1) que pertencem ao conjunto de propriedades.  
  
5.  Preencher a estrutura DBPROP para cada propriedade.  
  
6.  Preencher as informações (GUID do conjunto de propriedades, contagem do número de elementos e um ponteiro para a matriz DBPROP correspondente) na estrutura DBPROPSET para cada conjunto de propriedades.  
  
7.  Chamar um método para definir propriedades e passar a contagem e a matriz de estruturas DBPROPSET.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um aplicativo do OLE DB Driver for SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [Propriedades (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=112207)  
  
  

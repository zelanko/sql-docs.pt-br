---
title: Atualizado - documentos de bancos de dados relacionais | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado recentemente alterada na documentação de, para bancos de dados relacionais."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 3ab051a6fd00670139bb1089dcd3f4af76b9ecef
ms.contentlocale: pt-br
ms.lasthandoff: 05/25/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Novos e recentemente atualizado: documentos de bancos de dados relacionais



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2017-05-01** &nbsp; - para - &nbsp; **2017-05-23**
- *Área de assunto:* &nbsp; **bancos de dados relacionais**.




&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sqlgraphssql-graph-samplemd"></a>1. &nbsp;[Criar um banco de dados do gráfico e executar algumas consultas usando o T-SQL de correspondência de padrões](graphs/sql-graph-sample.md)

*Updated: 2017-05-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 68.  ms.author= "shkale".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ff467bf5fcf13592c796836def36e16e34f8cc31 99fcf0399006de16d0ac7cc9057564d307cb981b -->


```
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table, 
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 1), 
       (SELECT $node_id FROM Restaurant WHERE id = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 2), 
      (SELECT $node_id FROM Restaurant WHERE id = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 3), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 4), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 5), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 1),
      (SELECT $node_id FROM City WHERE id = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 2),
      (SELECT $node_id FROM City WHERE id = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 3),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 4),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 5),
      (SELECT $node_id FROM City WHERE id = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 1),
      (SELECT $node_id FROM City WHERE id =1));
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sysfngetauditfile-transact-sqlsystem-functionssys-fn-get-audit-file-transact-sqlmd"></a>2. &nbsp; [sys. fn_get_audit_file (Transact-SQL)](system-functions/sys-fn-get-audit-file-transact-sql.md)

*Updated: 2017-05-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 046fa92ad1b7e6bb7a956493ca06cf72d45b5285 fbf55361da90663835d7e107fda697c358e0e061 -->



- **Banco de Dados SQL do Azure**

  Este exemplo lê de um arquivo chamado `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  Este exemplo lê todos os logs dos servidores que começam com de auditoria `Sh`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```





&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd"></a>3. &nbsp;[Gerenciar a retenção de dados históricos em tabelas temporais com versão do sistema](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b -->



**Usando a abordagem de política de retenção de histórico Temporal**

> **Observação:** usando a política de retenção de histórico Temporal abordagem aplica-se a [! INCLUIR [sqldbesa-... /.. /Includes/sqldbesa-MD.MD]) e a partir do CTP 1.3 de 2017 do SQL Server.  

Retenção de histórico temporal pode ser configurado no nível de tabela individuais, que permite aos usuários criar vencimento flexível políticas. A aplicação de retenção temporal é simple: requer apenas um parâmetro a ser definido durante a alteração de esquema ou criação de tabela.

Depois de definir a política de retenção, o banco de dados do SQL Azure inicia verificando regularmente se há linhas de histórico que são qualificadas para a limpeza automática de dados. Identificação de linhas correspondentes e sua remoção da tabela de histórico ocorrem de modo transparente, na tarefa em segundo plano que é programada e executada pelo sistema. Condição de idade para as linhas da tabela de histórico é verificada com base na coluna que representa o final do período SYSTEM_TIME. Se o período de retenção, por exemplo, é definido como seis meses, linhas de tabela qualificadas para limpeza atendem a seguinte condição:
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
No exemplo anterior, supomos que a coluna de ValidTo corresponde ao final do período SYSTEM_TIME.
**Como configurar a política de retenção?**

Antes de configurar a política de retenção para uma tabela temporal, verifique primeiro se a retenção de histórico temporal está habilitada no nível do banco de dados:
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
Sinalizador de banco de dados **is_temporal_history_retention_enabled** é definida como ON, por padrão, mas os usuários podem alterá-lo com a instrução ALTER DATABASE. Automaticamente, ela é definida como OFF após ponto na operação de restauração do tempo. Para ativar a limpeza de retenção de histórico temporal para seu banco de dados, execute a seguinte instrução:
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
Política de retenção é configurada durante a criação de uma tabela especificando o valor do parâmetro HISTORY_RETENTION_PERIOD:
```
CREATE TABLE dbo.WebsiteUserInfo
```





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção anterior.

1. [Criar um banco de dados do gráfico e executar algumas consultas usando o T-SQL de correspondência de padrões](#TitleNum_1)
2. [sys. fn_get_audit_file (Transact-SQL)](#TitleNum_2)
3. [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](#TitleNum_3)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>Artigos irmã

Esta seção lista os artigos muito semelhantes para artigos atualizados recentemente em outras áreas de assunto, dentro do mesmo repositório GitHub.


&nbsp;

[Microsoft /**sql de documentos de pr** ](https://github.com/microsoftdocs/sql-docs-pr/) repositório em GitHub.com:

- [Atualizado recentemente: **bancos de dados relacionais e o Microsoft SQL Server** documentos](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [Atualizado recentemente: **Microsoft SQL Server** documentos](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [Atualizado recentemente: **Transact-SQL no SQL Server** documentos](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;




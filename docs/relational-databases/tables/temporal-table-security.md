---
description: Segurança da tabela temporal
title: Segurança de tabela temporal | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 60e5d6f6-a26d-4bba-aada-42e382bbcd38
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5dbfd363746a0849643835d3d9cf567c8f065e7f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463717"
---
# <a name="temporal-table-security"></a>Segurança da tabela temporal

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Para compreender como a segurança se aplica às tabelas temporais, é importante entender as entidades de segurança que se aplicam a elas. Quando entender esses princípios, você estará pronto para saber mais sobre a segurança das instruções **CREATE TABLE**, **ALTER TABLE**e **SELECT** .

## <a name="security-principles"></a>Princípios de segurança

 A tabela a seguir descreve os princípios de segurança que se aplicam às tabelas temporais:

|Princípio|DESCRIÇÃO|
|---------------|-----------------|
|Habilitar/desabilitar a determinação de versão do sistema requer privilégios mais altos sobre os objetos afetados|Habilitar e desabilitar SYSTEM_VERSIONING requer a permissão CONTROL na tabela atual e na tabela do histórico|
|Os dados do histórico não podem ser modificados diretamente|Quando SYSTEM_VERSIONING está ATIVADO, os usuários não podem alterar os dados do histórico, independentemente de suas permissões reais na tabela atual ou na tabela do histórico. Isso inclui as modificações dos dados e do esquema.|
|Consultar dados de histórico requer a permissão **SELECT** para a tabela do histórico|Ter apenas a permissão **SELECT** para a tabela atual não implica em ter a permissão **SELECT** para a tabela do histórico.|
|Operações de auditoria de superfície que afetam a tabela do histórico de formas específicas:|As configurações de auditoria da tabela atual não são automaticamente aplicadas à tabela de histórico. A auditoria precisa ser habilitada explicitamente para a tabela de histórico.<br /><br /> Depois de habilitada, a auditoria na tabela de histórico captura regularmente todas as tentativas diretas de acessar os dados (independentemente de serem bem-sucedidas ou não).<br /><br /> A permissão**SELECT** com a extensão de consulta temporal mostra que a tabela do histórico foi afetada com essa operação.<br /><br /> A tabela temporal**CREATE/ALTER** que expõe informações verificadas por essa permissão também ocorre na tabela do histórico. O arquivo de auditoria inclui um registro adicional para a tabela do histórico.<br /><br /> As operações de DML na superfície da tabela atual cuja tabela do histórico foi afetada, exceto additional_info, fornecem o contexto necessário (DML foi resultado de system_versioning).|

## <a name="performing-schema-operations"></a>Executando operações de esquema

Quando SYSTEM_VERSIONING é definido como ATIVO, as operações de modificação do esquema são limitadas.

### <a name="disallowed-alter-schema-operations"></a>Operações de esquema ALTER não permitidas

|Operação|Tabela atual|Tabela de histórico|
|---------------|-------------------|-------------------|
|**DROP TABLE**|Não permitido|Não permitido|
|**ALTER TABLE...SWITCH PARTITION**|Somente SWITCH IN (veja [Particionamento de tabelas temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md))|Somente SWITCH OUT (veja [Particionamento de tabelas temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md))|
|**ALTER TABLE...DROP PERIOD**|Não permitido|-|
|**ALTER TABLE...ADD PERIOD**|-|Não permitido|

## <a name="allowed-alter-table-operations"></a>Operações ALTER TABLE permitidas

|Operação|Current|Histórico|
|---------------|-------------|-------------|
|**ALTER TABLE...REBUILD**|Permitido (de forma independente)|Permitido (de forma independente)|
|**CREATE INDEX**|Permitido (de forma independente)|Permitido (de forma independente)|
|**CREATE STATISTICS**|Permitido (de forma independente)|Permitido (de forma independente)|

## <a name="security-of-the-create-temporal-table-statement"></a>Segurança da instrução CREATE Temporal TABLE

| Recurso | Criar nova tabela de histórico | Reutilizar tabela de histórico existente |
| ------- | ------------------------ | ---------------------------- |
|Permissão necessária|Permissão**CREATE TABLE** no banco de dados<br /><br /> Permissão**ALTER** para os esquemas nos quais a tabela atual e a tabela do histórico são criadas.|Permissão**CREATE TABLE** no banco de dados<br /><br /> Permissão**ALTER** para o esquema no qual a tabela atual será criada.<br /><br /> Permissão**CONTROL** para a tabela de histórico especificada como parte da instrução **CREATE TABLE** que cria a tabela temporal|
|Audit|A auditoria mostra que os usuários tentaram criar dois objetos. A operação pode falhar devido à falta de permissões para criar uma tabela no banco de dados ou devido à falta de permissões para alterar os esquemas dessa tabela.|Auditoria mostra que a tabela temporal foi criada. A operação pode falhar devido à falta de permissão para criar uma tabela no banco de dados, devido à falta de permissões para alterar o esquema da tabela temporal ou à falta de permissões na tabela do histórico.|

## <a name="security-of-the-alter-temporal-table-set-system_versioning-onoff-statement"></a>Segurança da instrução ALTER Temporal TABLE SET (SYSTEM_VERSIONING ATIVADO/DESATIVADO)

| Recurso | Criar nova tabela de histórico | Reutilizar tabela de histórico existente |
| ------- | ------------------------ | ---------------------------- |
|Permissão necessária|Permissão**CONTROL** no banco de dados<br /><br /> Permissão**CREATE TABLE** no banco de dados<br /><br /> Permissão**ALTER** para os esquemas nos quais a tabela do histórico é criada|Permissão**CONTROL** para a tabela original que foi alterada<br /><br /> Permissão**CONTROL** para a tabela de histórico especificada como parte da instrução **ALTER TABLE**|
|Audit|A auditoria mostra que a tabela temporal foi alterada e a tabela do histórico foi criada ao mesmo tempo. A operação pode falhar devido à falta de permissões para criar uma tabela no banco de dados, devido à falta de permissões para alterar o esquema da tabela de histórico ou à falta de permissão para modificar a tabela temporal.|A auditoria mostra que a tabela temporal foi alterada, mas a operação requer acesso para a tabela do histórico. A operação pode falhar devido à falta de permissões para a tabela do histórico ou para a tabela atual.|

## <a name="security-of-select-statement"></a>Segurança da instrução SELECT

A permissão**SELECT** é inalterada para as instruções **SELECT** que não afetam a tabela do histórico. Para as instruções **SELECT** que afetam a tabela do histórico, a permissão **SELECT** é necessária para a tabela atual e para a tabela do histórico.

## <a name="see-also"></a>Consulte Também

- [Tabelas temporais](../../relational-databases/tables/temporal-tables.md) 
- [Introdução a tabelas temporais com controle da versão do sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Particionamento com tabelas temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)

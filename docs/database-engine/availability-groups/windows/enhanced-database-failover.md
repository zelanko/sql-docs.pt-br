---
title: "Adicionar um failover de banco de dados avançado a um grupo de disponibilidade (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: mikeray
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], enhanced database failover
- Availability Groups [SQL Server], failover
ms.assetid: 
caps.latest.revision: 
author: allanhirt
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2050eed47dbe036cf0b51c9acb3fb823f4c6fa60
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="add-enhanced-database-failover-to-an-availability-group-sql-server"></a>Adicionar um failover de banco de dados avançado a um grupo de disponibilidade (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

No SQL Server 2012 e 2014, se um banco de dados que faz parte de um grupo de disponibilidade na réplica primária perder a capacidade de gravar as transações, ele não disparará um failover, mesmo se as réplicas estiverem sincronizadas e configuradas para failover automático.

O SQL Server 2016 introduz um novo comportamento opcional chamado *failover de banco de dados avançado* que pode ser definido pelo Assistente ou com o Transact-SQL. Se essa opção estiver habilitada e o failover automático for configurado, quando um banco de dados que faz parte de um grupo de disponibilidade não puder mais gravar transações, isso disparará um failover em uma réplica secundária sincronizada.

**Cenário 1**

Um grupo de disponibilidade é configurado entre a Instância A e a Instância B, que contém um banco de dados individual chamado DB1. O arquivo de dados do DB1 está na Unidade E e seu arquivo de log de transações está na Unidade f. O modo de disponibilidade é definido como confirmação síncrona com failover automático. A nova opção de failover de banco de dados avançado é configurada no grupo de disponibilidade. As duas réplicas estão em um estado sincronizado no momento. Um problema faz com que a Unidade E falhe. Esse cenário não causará um failover de banco de dados avançado, pois a Unidade E não contém o log de transações.  

**Cenário 2**

Isso tem a mesma configuração de grupo de disponibilidade do Cenário 1. Em vez da Unidade E falhar, desta vez, a unidade do log de transações, Unidade F, falha. Isso disparará um failover, pois atende à condição abrangida pelo failover de banco de dados avançado: o log de transações não está acessível, o que significa que o banco de dados não pode gravar transações.

**Cenário 3**

Um grupo de disponibilidade é configurado entre a Instância A e a Instância B, que contém dois bancos de dados: DB1 e DB2. O modo de disponibilidade é definido como confirmação síncrona com um modo de failover automático e o failover de banco de dados avançado está habilitado. O acesso ao disco que contém dados e os arquivos de log de transações do DB2 é perdido. Quando o problema for detectado, o grupo de disponibilidade fará failover automaticamente para a Instância B.

## <a name="configure-and-view-the-enhanced-database-failover-option"></a>Configurar e exibir a opção de failover de banco de dados avançado

O failover de banco de dados avançado pode ser configurado com o SQL Server Management Studio ou o Transact-SQL. Atualmente, os cmdlets do PowerShell não têm essa capacidade. Por padrão, o failover de banco de dados avançado está desabilitado.

### <a name="sql-server-management-studio"></a>SQL Server Management Studio

É possível habilitar o failover de banco de dados avançado durante a criação de um grupo de acessibilidade usando o SQL Server Management Studio. A única maneira de desabilitá-lo ou habilitá-lo depois de criar o grupo de disponibilidade é usar o Transact-SQL.

*Criação manual de grupo de disponibilidade*

Use as instruções encontradas no artigo [Usar a caixa de diálogo Novo Grupo de Disponibilidade (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md) para criar o grupo de disponibilidade. Para habilitar o failover de banco de dados avançado, marque sua caixa de seleção ao lado de *Detecção de Integridade no Nível do Banco de Dados*.

*Usando o Assistente de Grupo de Disponibilidade*

Use as instruções encontradas no artigo [Usar o Assistente de Grupo de Disponibilidade (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md). A opção para habilitar o failover de banco de dados avançado foi encontrada na caixa de diálogo Especificar Nome do Grupo de Disponibilidade. Para habilitá-la, marque a caixa ao lado de *Detecção de Integridade no Nível do Banco de Dados*.

### <a name="transact-sql"></a>Transact-SQL

Para configurar o comportamento de failover de banco de dados avançado durante a criação de um grupo de disponibilidade, DB_FAILOVER deve ser definido como ON, da seguinte maneira:

```SQL
CREATE AVAILABILITY GROUP [AGNAME]
WITH ( DB_FAILOVER = ON)
...
```
Para adicionar esse comportamento depois que um grupo de disponibilidade for configurado, use o comando ALTER AVAILABILITY GROUP:
```SQL
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = ON)
```
Para desabilitar esse comportamento, emita o seguinte comando ALTER AVAILABILITY GROUP:
```SQL
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = OFF)
```
### <a name="dynamic-management-view"></a>Exibição de gerenciamento dinâmico
Para ver se um grupo de disponibilidade foi habilitado para o failover de banco de dados avançado, consulte a exibição de gerenciamento dinâmico `sys.availability_groups`. A coluna `db_failover` terá um zero se ele estiver desabilitado ou 1 se estiver habilitado. 

## <a name="next-steps"></a>Próximas etapas 

- [Configurar a detecção de integridade do banco de dados](sql-server-always-on-database-health-detection-failover-option.md)

- [Usar o Assistente de Grupo de Disponibilidade (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

- [Usar a caixa de diálogo Novo Grupo de Disponibilidade (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
- [Criar um grupo de disponibilidade com o Transact-SQL](create-an-availability-group-transact-sql.md)


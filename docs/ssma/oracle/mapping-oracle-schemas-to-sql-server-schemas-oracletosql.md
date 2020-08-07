---
title: Mapeando esquemas Oracle para esquemas de SQL Server (OracleToSQL) | Microsoft Docs
description: Saiba como personalizar o SSMA para mapeamentos Oracle entre esquemas Oracle e SQL Server ou aceite o padrão.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 8d9511ae5c6d5a937e3686d0db45c578aec151c3
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934715"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Mapeamento de esquemas do Oracle para esquemas do SQL Server (OracleToSQL)
No Oracle, cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos em um esquema Oracle para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados chamado para o esquema. No entanto, você pode personalizar o mapeamento entre esquemas e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados Oracle.  
  
## <a name="oracle-and-sql-server-schemas"></a>Esquemas do Oracle e do SQL Server  
Um banco de dados Oracle contém esquemas. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém vários bancos de dados, cada um deles pode ter vários esquemas.  
  
O conceito da Oracle de um esquema é mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conceito de um banco de dados e de um de seus esquemas. Por exemplo, o Oracle pode ter um esquema chamado **HR**. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ter um banco de dados chamado **HR**e, nesse banco de dados, são esquemas. Um esquema é o esquema de **dbo** (ou proprietário do banco de dados). Por padrão, a **HR** do esquema Oracle será mapeada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados e o esquema **hr. dbo**. O SSMA se refere à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinação de banco de dados e esquema como um esquema.  
  
Você pode modificar o mapeamento entre Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e o banco de dados de destino  
No SSMA, você pode mapear um esquema Oracle para qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema disponível.  
  
**Para modificar o banco de dados e o esquema**  
  
1.  No Gerenciador de metadados Oracle, selecione **esquemas**.  
  
    A guia **mapeamento de esquema** também está disponível quando você seleciona um banco de dados individual, a pasta **esquemas** ou esquemas individuais. A lista na guia **mapeamento de esquema** é personalizada para o objeto selecionado.  
  
2.  No painel direito, clique na guia **mapeamento de esquema** .  
  
    Você verá uma lista de todos os esquemas Oracle, seguida por um valor de destino. Esse destino é indicado em uma notação de duas partes (*Database. Schema*) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seus objetos e dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e clique em **Modificar**.  
  
    Na caixa de diálogo **escolher esquema de destino** , você pode procurar o banco de dados de destino e o esquema disponíveis ou digitar o banco de dados e o nome do esquema na caixa de texto em uma notação de duas partes (Database. Schema) e clicar em **OK**.  
  
4.  O destino é alterado na guia **mapeamento de esquema** .  
  
**Modos de mapeamento**  
  
-   Mapeando para SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão, banco de dados de origem é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o banco de dados de destino com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado não for existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você será solicitado com uma mensagem **"o banco de dados e/ou esquema não existe nos metadados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim. Da mesma forma, você pode mapear o esquema para um esquema não existente no banco de dados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que será criado durante a sincronização.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados e esquema padrão  
Se você personalizar o mapeamento entre um esquema Oracle e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema, poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados e o esquema padrão**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados e o esquema padrão.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você quiser analisar a conversão de objetos Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, poderá [criar um relatório de conversão](assessing-oracle-schemas-for-conversion-oracletosql.md). Caso contrário, você pode [converter as definições de objeto do banco de dados Oracle](converting-oracle-schemas-oracletosql.md) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto.  
  
## <a name="see-also"></a>Consulte Também  
[Conectando-se ao SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

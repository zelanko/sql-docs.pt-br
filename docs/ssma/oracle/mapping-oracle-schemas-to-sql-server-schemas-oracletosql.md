---
title: Mapeando esquemas Oracle para esquemas de SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e375c07ceddc995b599930c14f00710af040d6c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68262909"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Mapeamento de esquemas do Oracle para esquemas do SQL Server (OracleToSQL)
No Oracle, cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos em um esquema Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um banco de dados chamado para o esquema. No entanto, você pode personalizar o mapeamento entre esquemas e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados Oracle.  
  
## <a name="oracle-and-sql-server-schemas"></a>Esquemas do Oracle e do SQL Server  
Um banco de dados Oracle contém esquemas. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém vários bancos de dados, cada um deles pode ter vários esquemas.  
  
O conceito da Oracle de um esquema é mapeado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o conceito de um banco de dados e de um de seus esquemas. Por exemplo, o Oracle pode ter um esquema chamado **HR**. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ter um banco de dados chamado **HR**e, nesse banco de dados, são esquemas. Um esquema é o esquema de **dbo** (ou proprietário do banco de dados). Por padrão, a **HR** do esquema Oracle será mapeada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados e o esquema **hr. dbo**. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA se refere à combinação de banco de dados e esquema como um esquema.  
  
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
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão, banco de dados de origem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é mapeado para o banco de dados de destino com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não for existente no, você será solicitado com uma mensagem **"o banco de dados e/ou esquema não existe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos metadados de destino. Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim. Da mesma forma, você pode mapear o esquema para um esquema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não existente no banco de dados de destino que será criado durante a sincronização.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados e esquema padrão  
Se você personalizar o mapeamento entre um esquema Oracle e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema, poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados e o esquema padrão**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados e o esquema padrão.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você quiser analisar a conversão de objetos Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, poderá [criar um relatório de conversão](assessing-oracle-schemas-for-conversion-oracletosql.md). Caso contrário, você pode [converter as definições de objeto do banco de dados Oracle](converting-oracle-schemas-oracletosql.md) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto.  
  
## <a name="see-also"></a>Consulte Também  
[Conectando-se ao SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

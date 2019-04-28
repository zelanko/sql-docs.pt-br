---
title: Mapeando esquemas Oracle para esquemas do SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 61b706145f708e9b2e8a04ba4e7bc574c503a742
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62795780"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Mapeamento de esquemas do Oracle para esquemas do SQL Server (OracleToSQL)
No Oracle, cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos em um esquema do Oracle para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nomeado para o esquema de banco de dados. No entanto, você pode personalizar o mapeamento entre esquemas Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle e esquemas do SQL Server  
Um banco de dados Oracle contém esquemas. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém vários bancos de dados, cada um deles pode ter vários esquemas.  
  
O conceito de Oracle de um esquema é mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conceito de um banco de dados e um dos seus esquemas. Por exemplo, Oracle pode ter um esquema chamado **HR**. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ter um banco de dados denominado **HR**, e dentro desse banco de dados são esquemas. Um esquema é o **dbo** (ou proprietário de banco de dados) esquema. Por padrão, o esquema do Oracle **HR** serão mapeados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados e esquema **HR.dbo**. O SSMA refere-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinação de esquema e banco de dados como um esquema.  
  
Você pode modificar o mapeamento entre Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e banco de dados de destino  
No SSMA, você pode mapear um esquema do Oracle para qualquer disponíveis [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema.  
  
**Para modificar o esquema e banco de dados**  
  
1.  No Gerenciador de metadados do Oracle, selecione **esquemas**.  
  
    O **esquema de mapeamento** guia também está disponível quando você seleciona um banco de dados individual, o **esquemas** pasta ou esquemas individuais. Na lista de **esquema de mapeamento** guia personalizada para o objeto selecionado.  
  
2.  No painel direito, clique no **esquema de mapeamento** guia.  
  
    Você verá uma lista de todos os esquemas do Oracle, seguido por um valor de destino. Este destino é indicado em uma notação de duas partes (*database.schema*) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde seus objetos e dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e, em seguida, clique em **modificar**.  
  
    No **escolha o esquema de destino** caixa de diálogo, você pode navegar para o banco de dados de destino disponíveis e o esquema ou o tipo de banco de dados e esquema de nome na caixa de texto em uma notação de duas partes (database.schema) e, em seguida, clique em **Okey**.  
  
4.  O destino é alterado na **esquema de mapeamento** guia.  
  
**Modos de mapeamento**  
  
-   Mapeamento para o SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão o banco de dados de origem é mapeado para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado é não existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em seguida, você receberá uma mensagem **"o banco de dados e/ou o esquema não existe no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Ele seria criado durante a sincronização. Você deseja continuar?"** Clique em Sim. Da mesma forma, você pode mapear o esquema para o esquema não existente no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados que será criado durante a sincronização.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados padrão e o esquema  
Se você personalizar o mapeamento entre um esquema do Oracle e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema, você poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados padrão e o esquema**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados padrão e o esquema.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você deseja analisar a conversão de objetos Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, você pode [criar um relatório de conversão](assessing-oracle-schemas-for-conversion-oracletosql.md). Caso contrário, você pode [converter as definições de objeto de banco de dados Oracle](converting-oracle-schemas-oracletosql.md) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto.  
  
## <a name="see-also"></a>Consulte também  
[Conectando ao SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Migrando do Oracle bancos de dados para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

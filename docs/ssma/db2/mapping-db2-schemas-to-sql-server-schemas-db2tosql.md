---
title: Mapeando esquemas do DB2 para esquemas do SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e9ccc7648be4915a68b798f314689d961113639a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298657"
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>Mapeando esquemas do DB2 para esquemas do SQL Server (DB2ToSQL)
No DB2, cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos em um esquema do DB2 para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nomeado para o esquema de banco de dados. No entanto, você pode personalizar o mapeamento entre os esquemas do DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 e esquemas do SQL Server  
Um banco de dados do DB2 contém esquemas. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém vários bancos de dados, cada um deles pode ter vários esquemas.  
  
O conceito de DB2 de um esquema é mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conceito de um banco de dados e um dos seus esquemas. Por exemplo, o DB2 pode ter um esquema chamado **HR**. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ter um banco de dados denominado **HR**, e dentro desse banco de dados são esquemas. Um esquema é o **dbo** (ou proprietário de banco de dados) esquema. Por padrão, o esquema do DB2 **HR** serão mapeados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados e esquema **HR.dbo**. O SSMA refere-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinação de esquema e banco de dados como um esquema.  
  
Você pode modificar o mapeamento entre o DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e banco de dados de destino  
No SSMA, você pode mapear um esquema do DB2 para alguma disponível [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema.  
  
**Para modificar o esquema e banco de dados**  
  
1.  No Gerenciador de metadados do DB2, selecione **esquemas**.  
  
    O **esquema de mapeamento** guia também está disponível quando você seleciona um banco de dados individual, o **esquemas** pasta ou esquemas individuais. Na lista de **esquema de mapeamento** guia personalizada para o objeto selecionado.  
  
2.  No painel direito, clique no **esquema de mapeamento** guia.  
  
    Você verá uma lista de todos os esquemas do DB2, seguido por um valor de destino. Este destino é indicado em uma notação de duas partes (*database.schema*) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde seus objetos e dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e, em seguida, clique em **modificar**.  
  
    No **escolha o esquema de destino** caixa de diálogo, você pode navegar para o banco de dados de destino disponíveis e o esquema ou o tipo de banco de dados e esquema de nome na caixa de texto em uma notação de duas partes (database.schema) e, em seguida, clique em **Okey**.  
  
4.  O destino é alterado na **esquema de mapeamento** guia.  
  
**Modos de mapeamento**  
  
-   Mapeamento para o SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão o banco de dados de origem é mapeado para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado é não existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em seguida, você receberá uma mensagem **"o banco de dados e/ou o esquema não existe no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Ele seria criado durante a sincronização. Você deseja continuar?"** Clique em Sim. Da mesma forma, você pode mapear o esquema para o esquema não existente no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados que será criado durante a sincronização.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados padrão e o esquema  
Se você personalizar o mapeamento entre um esquema do DB2 e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema, você poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados padrão e o esquema**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados padrão e o esquema.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você deseja analisar a conversão de DB2 objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, você pode [relatório de migração de dados (SSMA comuns)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241).  
  
## <a name="see-also"></a>Consulte também  
[Conectando ao SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[Bancos de dados do DB2 migrando para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

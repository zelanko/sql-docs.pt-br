---
title: Mapeando esquemas do DB2 para esquemas de SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 50845a9bdf3c3185d7b69bb86a75b2a3d332ef6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68074171"
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>Mapeando esquemas do DB2 para esquemas de SQL Server (DB2ToSQL)
No DB2, cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos em um esquema do DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um banco de dados chamado para o esquema. No entanto, você pode personalizar o mapeamento entre os esquemas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e bancos de dados do DB2.  
  
## <a name="db2-and-sql-server-schemas"></a>Esquemas DB2 e SQL Server  
Um banco de dados DB2 contém esquemas. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém vários bancos de dados, cada um deles pode ter vários esquemas.  
  
O conceito de DB2 de um esquema é mapeado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o conceito de um banco de dados e de um de seus esquemas. Por exemplo, o DB2 pode ter um esquema chamado **HR**. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ter um banco de dados chamado **HR**e, nesse banco de dados, são esquemas. Um esquema é o esquema de **dbo** (ou proprietário do banco de dados). Por padrão, a **HR** do esquema do DB2 será mapeada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o banco de dados e o esquema **hr. dbo**. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA se refere à combinação de banco de dados e esquema como um esquema.  
  
Você pode modificar o mapeamento entre DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e o banco de dados de destino  
No SSMA, você pode mapear um esquema do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qualquer esquema disponível.  
  
**Para modificar o banco de dados e o esquema**  
  
1.  No Gerenciador de metadados do DB2, selecione **esquemas**.  
  
    A guia **mapeamento de esquema** também está disponível quando você seleciona um banco de dados individual, a pasta **esquemas** ou esquemas individuais. A lista na guia **mapeamento de esquema** é personalizada para o objeto selecionado.  
  
2.  No painel direito, clique na guia **mapeamento de esquema** .  
  
    Você verá uma lista de todos os esquemas do DB2, seguida por um valor de destino. Esse destino é indicado em uma notação de duas partes (*Database. Schema*) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seus objetos e dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e clique em **Modificar**.  
  
    Na caixa de diálogo **escolher esquema de destino** , você pode procurar o banco de dados de destino e o esquema disponíveis ou digitar o banco de dados e o nome do esquema na caixa de texto em uma notação de duas partes (Database. Schema) e clicar em **OK**.  
  
4.  O destino é alterado na guia **mapeamento de esquema** .  
  
**Modos de mapeamento**  
  
-   Mapeando para SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão, banco de dados de origem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é mapeado para o banco de dados de destino com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não for existente no, você será solicitado com uma mensagem **"o banco de dados e/ou esquema não existe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos metadados de destino. Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim. Da mesma forma, você pode mapear o esquema para um esquema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não existente no banco de dados de destino que será criado durante a sincronização.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados e esquema padrão  
Se você personalizar o mapeamento entre um esquema do DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um esquema, poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados e o esquema padrão**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados e o esquema padrão.  
  
## <a name="next-steps"></a>Próximas etapas  
Se desejar analisar a conversão de objetos DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, você poderá o relatório de migração de [dados (SSMA Common)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241).  
  
## <a name="see-also"></a>Consulte Também  
[Conectando-se ao SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[Migrar bancos de dados DB2 para SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

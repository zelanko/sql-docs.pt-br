---
title: Mapeamento de bancos de dados MySQL para esquemas SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6f6472656dbfd31ca64348d066cca19f303b4a5f
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>Mapeamento de bancos de dados MySQL para esquemas SQL Server (MySQLToSQL)
Por padrão, o SSMA para MySQL migra todos os objetos em um esquema do MySQL para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou nomeado para o esquema de banco de dados do SQL Azure. No entanto, você pode personalizar o mapeamento entre esquemas de MySQL e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou bancos de dados do SQL Azure.  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL e SQL Server ou SQL Azure esquemas  
O conceito de MySQL de um esquema é mapeado para o conceito de SQL Server de um banco de dados e um de seus esquemas. O SSMA refere-se a combinação do SQL Server do banco de dados e esquema como um esquema.  
  
O conceito de MySQL de um esquema é mapeado para o conceito de SQL Server de um banco de dados e um de seus esquemas. Por exemplo, o MySQL pode ter um esquema denominado **HR**. Uma instância do SQL Server pode ter um banco de dados denominado **HR**, e são os esquemas no banco de dados. Um esquema é o **dbo** (ou proprietário de banco de dados) esquema. Por padrão, o esquema MySQL **HR** será mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados e esquema **HR.dbo**. O SSMA refere-se para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] combinação de banco de dados e esquema como um esquema.  
  
Você pode modificar o mapeamento entre o MySQL e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas do Azure.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e banco de dados de destino  
No SSMA, você pode mapear um esquema MySQL para qualquer disponível [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquema do SQL Azure.  
  
**Para modificar o banco de dados e o esquema**  
  
1.  No Gerenciador de metadados do MySQL, selecione **esquemas**.  
  
    O **mapeamento de esquema** guia também está disponível quando você selecionar esquemas individuais. Na lista de **esquema de mapeamento** guia personalizada para o objeto selecionado.  
  
2.  No painel direito, clique no **mapeamento de esquema** guia.  
  
    Você verá uma lista de todos os esquemas do MySQL, seguido por um valor de destino. Esse destino é indicado em uma notação de duas partes (*database.schema*) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure em que seus objetos e os dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e, em seguida, clique em **modificar**.  
  
    No **esquema de destino escolha** caixa de diálogo, você pode navegar para o banco de dados de destino disponíveis e o esquema ou o tipo de banco de dados e esquema de nome na caixa de texto em uma notação de duas partes (database.schema) e, em seguida, clique em **Okey**.  
  
4.  O destino é alterado no **mapeamento de esquema** guia.  
  
**Modos de mapeamento**  
  
-   Mapeamento para o SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão o banco de dados de origem é mapeado para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado é inexistente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], em seguida, você receberá uma mensagem **"o banco de dados e/ou o esquema não existe no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados. Ele deve ser criado durante a sincronização. Deseja continuar?"** Clique em Sim. Da mesma forma, você pode mapear o esquema para o esquema não existente no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados que será criado durante a sincronização.  
  
-   Mapeamento para o SQL Azure  
  
Você pode mapear o banco de dados de origem para o destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados ou para qualquer esquema no destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Se você mapear o esquema de origem nenhum esquema não existente no banco de dados de destino conectados, você receberá uma mensagem **"esquema não existe nos metadados de destino. Ele deve ser criado durante a sincronização. Deseja continuar? "** Clique em Sim.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados padrão e o esquema  
Se você personalizar o mapeamento entre um esquema MySQL e um esquema do SQL Server, você poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados padrão e o esquema**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados padrão e o esquema.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você quiser analisar a conversão de objetos do MySQL em objetos do SQL Server ou SQL Azure, você pode [criar um relatório de conversão](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec) caso contrário, você pode [converter as definições de objeto de banco de dados MySQL](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7) em esquemas do SQL Server ou SQL Azure  
  
## <a name="see-also"></a>Consulte também  
[Configurações de projeto &#40; Conversão de &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Conectar-se ao banco de dados SQL do Azure &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[Migrando bancos de dados MySQL para o SQL Server - banco de dados SQL do Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Conectar-se ao SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  


---
title: Mapeamento de esquemas Oracle para esquemas SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2ca4fbcf3a49ccaf289bab39e3dbd15493fe08bb
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Mapeamento de esquemas Oracle para esquemas SQL Server (OracleToSQL)
No Oracle, cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos em um esquema do Oracle para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nomeado para o esquema de banco de dados. No entanto, você pode personalizar o mapeamento entre esquemas Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados.  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle e esquemas do SQL Server  
Um banco de dados Oracle contém esquemas. Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] contém vários bancos de dados, cada um deles pode ter vários esquemas.  
  
O conceito de Oracle de um esquema é mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conceito de um banco de dados e um de seus esquemas. Por exemplo, a Oracle pode ter um esquema denominado **HR**. Uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] pode ter um banco de dados denominado **HR**, e são os esquemas no banco de dados. Um esquema é o **dbo** (ou proprietário de banco de dados) esquema. Por padrão, o esquema do Oracle **HR** será mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados e esquema **HR.dbo**. O SSMA refere-se para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] combinação de banco de dados e esquema como um esquema.  
  
Você pode modificar o mapeamento entre o Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e banco de dados de destino  
No SSMA, você pode mapear um esquema do Oracle para qualquer disponível [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquema.  
  
**Para modificar o banco de dados e o esquema**  
  
1.  No Gerenciador de metadados do Oracle, selecione **esquemas**.  
  
    O **mapeamento de esquema** guia também está disponível quando você seleciona um banco de dados individual, o **esquemas** pasta ou esquemas individuais. Na lista de **esquema de mapeamento** guia personalizada para o objeto selecionado.  
  
2.  No painel direito, clique no **mapeamento de esquema** guia.  
  
    Você verá uma lista de todos os esquemas do Oracle, seguido por um valor de destino. Esse destino é indicado em uma notação de duas partes (*database.schema*) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onde seus objetos e os dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e, em seguida, clique em **modificar**.  
  
    No **esquema de destino escolha** caixa de diálogo, você pode navegar para o banco de dados de destino disponíveis e o esquema ou o tipo de banco de dados e esquema de nome na caixa de texto em uma notação de duas partes (database.schema) e, em seguida, clique em **Okey**.  
  
4.  O destino é alterado no **mapeamento de esquema** guia.  
  
**Modos de mapeamento**  
  
-   Mapeamento para o SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão o banco de dados de origem é mapeado para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado é inexistente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], em seguida, você receberá uma mensagem **"o banco de dados e/ou o esquema não existe no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados. Ele deve ser criado durante a sincronização. Deseja continuar?"** Clique em Sim. Da mesma forma, você pode mapear o esquema para o esquema não existente no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados que será criado durante a sincronização.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados padrão e o esquema  
Se você personalizar o mapeamento entre um esquema do Oracle e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquema, você poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados padrão e o esquema**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados padrão e o esquema.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você deseja analisar a conversão de objetos Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos, você pode [criar um relatório de conversão](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357). Caso contrário, você pode [converter as definições de objeto de banco de dados Oracle](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definições de objeto.  
  
## <a name="see-also"></a>Consulte também  
[Conectar-se ao SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Migrando bancos de dados Oracle para o SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  


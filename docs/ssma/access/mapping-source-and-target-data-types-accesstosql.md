---
title: Mapeamento de fonte e tipos de dados de destino (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a32f7f321baa17dbcdaf557bb7de033422a02dbc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740974"
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>Mapeamento de fonte e tipos de dados de destino (AccessToSQL)
Os tipos de banco de dados do Access variam de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de banco de dados. Quando você converte objetos de banco de dados de acesso à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, você deve especificar como mapear tipos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode aceitar os mapeamentos de tipo de dados padrão, ou você pode personalizar os mapeamentos conforme mostrado nos procedimentos a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto padrão de mapeamentos de tipo de dados. Para obter a lista de mapeamentos padrão, consulte [configurações do projeto (mapeamento de tipo)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655).  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
Usando o **configurações do projeto** caixa de diálogo, você pode personalizar como os tipos são mapeados para todos os bancos de dados e objetos de banco de dados em um projeto. Os mapeamentos de tipo para um projeto se aplicam a todos os bancos de dados e objetos de banco de dados que não têm mapeamentos de tipo personalizado.  
  
Você também pode personalizar o mapeamento de tipo de dados no nível do banco de dados ou tabela.  
  
O procedimento a seguir mostra como mapear tipos de dados no projeto, no banco de dados ou no nível de objeto de banco de dados.  
  
**Para mapear tipos de dados**  
  
1.  Para personalizar o mapeamento de tipo de dados para todo o projeto, abra o **configurações do projeto** caixa de diálogo:  
  
    1.  Sobre o **ferramentas** menu, selecione **configurações do projeto**.  
  
    2.  No painel esquerdo, selecione **mapeamento de tipo**.  
  
        O gráfico de mapeamento de tipo e os botões aparecem no painel direito.  
  
    Ou, para personalizar o mapeamento de tipo de dados no nível do banco de dados ou tabela, selecione o banco de dados ou tabela no painel Gerenciador de metadados de acesso:  
  
    1.  No painel de acesso Gerenciador de metadados, expanda **acesso metabase**e, em seguida, expanda **bancos de dados**.  
  
    2.  Selecione o banco de dados ou tabela para a qual você deseja personalizar o mapeamento de tipo de dados.  
  
    3.  No painel direito, clique em **mapeamento de tipo**.  
  
2.  Para adicionar um novo mapeamento, faça o seguinte:  
  
    1.  No painel de mapeamento de tipo, clique em **adicionar**.  
  
    2.  No **novo mapeamento de tipo** caixa de diálogo **tipo de fonte**, selecione o tipo de dados do Access para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique os comprimentos de dados mínimo e máximo para o mapeamento selecionando a **partir** e **para** caixas de seleção e, em seguida, inserir os valores.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Sob **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o comprimento de dados novo na **substituir por** caixa e, em seguida, clique em **Okey**.  
  
3.  Para editar um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  No painel de mapeamento de tipo, clique em **editar**.  
  
    2.  No **a lista de mapeamento de tipo** caixa de diálogo **tipo de fonte**, selecione o tipo de dados do Access para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique os comprimentos de dados mínimo e máximo para o mapeamento selecionando a **partir** e **para** caixas de seleção e, em seguida, inserir os valores.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Sob **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o comprimento de dados novo na **substituir por** caixa e, em seguida, clique em **Okey**.  
  
4.  Para remover um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  No painel de mapeamento de tipo, selecione a linha na lista de mapeamento de tipo que contém o mapeamento de tipo de dados que deseja remover.  
  
    2.  Clique em **Remover**.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa no processo de migração é [converter objetos de banco de dados do access para objetos do SQL Server](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  

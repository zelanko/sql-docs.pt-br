---
title: Mapeamento de fonte e tipos de dados de destino (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3bb6bd72d6b20ef207653b904607a9df942c2858
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>Mapeamento de fonte e tipos de dados de destino (AccessToSQL)
Os tipos de banco de dados do Access variam de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de banco de dados. Ao converter objetos de banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos, você deve especificar como mapear tipos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você pode aceitar os mapeamentos de tipo de dados padrão, ou você pode personalizar os mapeamentos conforme mostrado nos procedimentos a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto de mapeamentos de tipo de dados padrão. Para obter a lista de mapeamentos padrão, consulte [configurações do projeto (tipo de mapeamento)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655).  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
Usando o **configurações de projeto** caixa de diálogo, você pode personalizar como os tipos são mapeados para todos os bancos de dados e objetos de banco de dados em um projeto. Os mapeamentos de tipo para um projeto se aplicam a todos os bancos de dados e objetos de banco de dados que não têm mapeamentos de tipo personalizado.  
  
Você também pode personalizar o mapeamento de tipo de dados no nível do banco de dados ou tabela.  
  
O procedimento a seguir mostra como mapear tipos de dados no projeto, no banco de dados ou no nível de objeto de banco de dados.  
  
**Para mapear tipos de dados**  
  
1.  Para personalizar o mapeamento de tipo de dados para o projeto inteiro, abra o **configurações de projeto** caixa de diálogo:  
  
    1.  Sobre o **ferramentas** menu, selecione **configurações de projeto**.  
  
    2.  No painel esquerdo, selecione **mapeamento de tipo**.  
  
        Os botões e o gráfico de mapeamento de tipo aparecem no painel direito.  
  
    Ou, para personalizar o mapeamento de tipo de dados no nível do banco de dados ou tabela, selecione o banco de dados ou uma tabela no painel Explorador de metadados de acesso:  
  
    1.  No painel de acesso Gerenciador de metadados, expanda **acesso metabase**e, em seguida, expanda **bancos de dados**.  
  
    2.  Selecione o banco de dados ou tabela para a qual você deseja personalizar o mapeamento de tipo de dados.  
  
    3.  No painel direito, clique em **mapeamento de tipo**.  
  
2.  Para adicionar um novo mapeamento, faça o seguinte:  
  
    1.  No painel de mapeamento de tipo, clique em **adicionar**.  
  
    2.  No **novo mapeamento de tipo** caixa de diálogo **tipo de fonte**, selecione o tipo de dados do Access para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique os comprimentos de dados mínimo e máximo para o mapeamento selecionando o **de** e **para** caixas de seleção e, em seguida, inserir os valores.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados.  
  
        Alguns tipos de exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento de dados no **substituir por** caixa e, em seguida, clique em **Okey**.  
  
3.  Para editar um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  No painel de mapeamento de tipo, clique em **editar**.  
  
    2.  No **a lista de mapeamento de tipo** caixa de diálogo **tipo de fonte**, selecione o tipo de dados do Access para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique os comprimentos de dados mínimo e máximo para o mapeamento selecionando o **de** e **para** caixas de seleção e, em seguida, inserir os valores.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados.  
  
        Alguns tipos de exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento de dados no **substituir por** caixa e, em seguida, clique em **Okey**.  
  
4.  Para remover um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  No painel de mapeamento de tipo, selecione a linha na lista de mapeamento de tipo que contém o mapeamento de tipo de dados que deseja remover.  
  
    2.  Clique em **Remover**.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa no processo de migração é [converter objetos de banco de dados de acesso a objetos do SQL Server](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

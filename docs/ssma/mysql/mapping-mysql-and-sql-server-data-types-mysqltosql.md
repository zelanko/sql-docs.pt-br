---
title: Mapeamento de tipos de dados do SQL Server (MySQLToSQL) e o MySQL | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee34e34e1b0048fd1cb15744cc215962e5a563e5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>Mapeamento de tipos de dados do SQL Server (MySQLToSQL) e MySQL
Os tipos de banco de dados MySQL variam de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tipos de banco de dados do SQL Azure. Ao converter objetos de banco de dados MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure, você deve especificar como mapear tipos de dados do MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você pode aceitar os mapeamentos de tipo de dados padrão, ou você pode personalizar os mapeamentos conforme mostrado nos procedimentos a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto de mapeamentos de tipo de dados padrão. Para obter a lista de mapeamentos padrão, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de mapeamento de herança  
Você pode personalizar mapeamentos de tipo no nível de projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível mais alto, a menos que elas são substituídas em um nível inferior. Por exemplo, se você mapear **smallint** para **int** no nível de projeto, todos os objetos no projeto usará esse mapeamento, a menos que você personalize o mapeamento no nível do objeto ou categoria.  
  
Quando você exibe o **mapeamento de tipo** guia SSMA, o plano de fundo é codificadas por cor para mostrar os mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
  
-   **Para mapear tipos de dados:**  
  
    Os procedimentos a seguir mostram como mapear tipos de dados no projeto, no banco de dados ou no nível de objeto de banco de dados:  
  
    1.  Para personalizar o mapeamento de tipo de dados para o projeto inteiro, abra o **configurações de projeto** caixa de diálogo. No menu Ferramentas, selecione **configurações de projeto**.  
  
        No painel esquerdo, selecione **mapeamento de tipo**. Os botões e o gráfico de mapeamento de tipo aparecem no painel direito.  
  
    2.  Para personalizar os mapeamentos de tipo de dados no nível do banco de dados ou tabela, selecione o banco de dados ou uma tabela no Gerenciador de metadados de MySQL. No Gerenciador de metadados de MySQL, selecione a pasta ou o objeto para personalizar.  
  
        No painel direito, clique em **mapeamento de tipo**.  
  
-   **Para adicionar um novo mapeamento, faça o seguinte:**  
  
    1.  No painel de mapeamento de tipo, clique em **adicionar** .  
  
    2.  No novo tipo de caixa de diálogo de mapeamento em **tipo de fonte**, selecione o tipo de dados MySQL para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique os comprimentos de dados mínimo e máximo para o mapeamento selecionando o **de** e **para** caixas de seleção e, em seguida, inserir os valores.  
  
    4.  Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados. Em **tipo de destino**, selecione o destino do SQL Server ou o tipo de dados do SQL Azure.  
  
        1.  Alguns tipos de exigem um comprimento de tipo de dados de destino. Se necessário, digite o novo comprimento de dados no **substituir por** caixa e, em seguida, clique em **Okey**.  
  
        2.  Alguns tipos requerem um tipo de dados de destino **precisão** e **escala**. Se necessário, insira a nova precisão e escala para o **substituir por** caixa e, em seguida, clique em **Okey**.  
  
-   **Para editar um mapeamento de tipo, faça o seguinte:**  
  
    1.  No painel de mapeamento de tipo, clique em **editar**.  
  
    2.  O mapeamento de tipo lista caixa de diálogo, em **tipo de fonte**, selecione o tipo de dados MySQL para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique os comprimentos de dados mínimo e máximo para o mapeamento selecionando o **de** e **para** caixas de seleção e, em seguida, inserir os valores.  
  
    Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados. Em **tipo de destino**, selecione o destino do SQL Server ou o tipo de dados do SQL Azure.  
  
    1.  Alguns tipos de exigem um comprimento de tipo de dados de destino. Se necessário, digite o novo comprimento de dados no **substituir por** caixa e, em seguida, clique em **Okey**.  
  
    2.  Alguns tipos requerem um tipo de dados de destino **precisão** e **escala** . Se necessário, insira a nova precisão e escala para o **substituir por** caixa e, em seguida, clique em **Okey** .  
  
-   **Para remover um mapeamento de tipo de dados, faça o seguinte:**  
  
    1.  No painel de mapeamento de tipo, selecione a linha na lista de mapeamento de tipo que contém o mapeamento de tipo de dados que deseja remover.  
  
    2.  Clique em **Remover**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é como [criar um relatório de avaliação](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec) ou [objetos de banco de dados MySQL converter em sintaxe de SQL Server ou SQL Azure](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7). Se você criar um relatório, os objetos de MySQL são automaticamente convertidos durante a avaliação.  
  
## <a name="see-also"></a>Consulte também  
[Bancos de dados MySQL migrando para o SQL Server - banco de dados SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

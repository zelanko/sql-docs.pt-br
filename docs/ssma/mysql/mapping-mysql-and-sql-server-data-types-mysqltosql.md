---
title: Mapeamento de MySQL e tipos de dados do SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 99e86d99a4214b1ccdf317e75218fe22bb2c7af7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908995"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>Mapear os tipos de dados do SQL Server e MySQL (MySQLToSQL)
Os tipos de banco de dados MySQL variam de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tipos de banco de dados do SQL Azure. Quando você converte objetos de banco de dados MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do SQL Azure, você deve especificar como mapear tipos de dados do MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode aceitar os mapeamentos de tipo de dados padrão, ou você pode personalizar os mapeamentos conforme mostrado nos procedimentos a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto padrão de mapeamentos de tipo de dados. Para obter a lista de mapeamentos padrão, consulte [configurações do projeto &#40;mapeamento de tipo&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de mapeamento de herança  
Você pode personalizar mapeamentos de tipo no nível do projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível mais alto, a menos que eles sejam substituídos em um nível inferior. Por exemplo, se você mapear **smallint** à **int** no nível do projeto, todos os objetos no projeto usará esse mapeamento, a menos que você personalize o mapeamento no nível do objeto ou categoria.  
  
Quando você exibe o **mapeamento de tipo** guia no SSMA, o plano de fundo é codificadas por cores para mostrar quais mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e, em branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
  
-   **Para mapear tipos de dados:**  
  
    Os procedimentos a seguir mostram como mapear tipos de dados no projeto, no banco de dados ou no nível de objeto de banco de dados:  
  
    1.  Para personalizar o mapeamento de tipo de dados para todo o projeto, abra o **configurações do projeto** caixa de diálogo. No menu Ferramentas, selecione **configurações do projeto**.  
  
        No painel esquerdo, selecione **mapeamento de tipo**. O gráfico de mapeamento de tipo e os botões aparecem no painel direito.  
  
    2.  Para personalizar mapeamentos de tipo de dados no nível do banco de dados ou tabela, selecione o banco de dados ou tabela no Gerenciador de metadados de MySQL. No Gerenciador de metadados de MySQL, selecione a pasta ou o objeto para personalizar.  
  
        No painel direito, clique em **mapeamento de tipo**.  
  
-   **Para adicionar um novo mapeamento, faça o seguinte:**  
  
    1.  No painel de mapeamento de tipo, clique em **adicionar** .  
  
    2.  No novo tipo de caixa de diálogo de mapeamento, em **tipo de fonte**, selecione o tipo de dados MySQL para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique os comprimentos de dados mínimo e máximo para o mapeamento selecionando a **partir** e **para** caixas de seleção e, em seguida, inserir os valores.  
  
    4.  Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados. Sob **tipo de destino**, selecione o destino do SQL Server ou o tipo de dados do SQL Azure.  
  
        1.  Alguns tipos exigem um comprimento de tipo de dados de destino. Se necessário, digite o novo comprimento de dados na **substituir por** caixa e, em seguida, clique em **Okey**.  
  
        2.  Alguns tipos exigem um tipo de dados de destino **precisão** e **escala**. Se necessário, insira a nova precisão e reduzir horizontalmente a **substituir por** caixa e, em seguida, clique em **Okey**.  
  
-   **Para editar um mapeamento de tipo, faça o seguinte:**  
  
    1.  No painel de mapeamento de tipo, clique em **editar**.  
  
    2.  No mapeamento de tipos de lista de caixa de diálogo, em **tipo de fonte**, selecione o tipo de dados MySQL para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique os comprimentos de dados mínimo e máximo para o mapeamento selecionando a **partir** e **para** caixas de seleção e, em seguida, inserir os valores.  
  
    Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados. Sob **tipo de destino**, selecione o destino do SQL Server ou o tipo de dados do SQL Azure.  
  
    1.  Alguns tipos exigem um comprimento de tipo de dados de destino. Se necessário, digite o novo comprimento de dados na **substituir por** caixa e, em seguida, clique em **Okey**.  
  
    2.  Alguns tipos exigem um tipo de dados de destino **precisão** e **escala** . Se necessário, insira a nova precisão e reduzir horizontalmente a **substituir por** caixa e, em seguida, clique em **Okey** .  
  
-   **Para remover um mapeamento de tipo de dados, faça o seguinte:**  
  
    1.  No painel de mapeamento de tipo, selecione a linha na lista de mapeamento de tipo que contém o mapeamento de tipo de dados que deseja remover.  
  
    2.  Clique em **Remover**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é para qualquer um dos [criar um relatório de avaliação](assessing-mysql-databases-for-conversion-mysqltosql.md) ou [MySQL converter objetos de banco de dados à sintaxe do SQL Server ou SQL Azure](converting-mysql-databases-mysqltosql.md). Se você criar um relatório, os objetos do MySQL são convertidos automaticamente durante a avaliação.  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

---
title: Mapeando MySQLToSQL (tipos de dados MySQL e SQL Server) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 604f9ce8e26e3d2221cd9a4bf7732c56ba3296c0
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935346"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>Mapear os tipos de dados do SQL Server e MySQL (MySQLToSQL)
Tipos de banco de dados MySQL diferem dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de banco de dados SQL ou do Azure Ao converter objetos do banco de dados MySQL em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos do ou SQL Azure, você deve especificar como mapear tipos de dado de MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode aceitar os mapeamentos de tipo de dados padrão ou pode personalizar os mapeamentos, conforme mostrado nos procedimentos a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto padrão de mapeamentos de tipo de dados. Para obter a lista de mapeamentos padrão, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
## <a name="type-mapping-inheritance"></a>Herança de mapeamento de tipo  
Você pode personalizar mapeamentos de tipo no nível de projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível superior, a menos que sejam substituídas em um nível inferior. Por exemplo, se você mapear **smallint** para **int** no nível do projeto, todos os objetos no projeto usarão esse mapeamento, a menos que você personalize o mapeamento no nível do objeto ou da categoria.  
  
Quando você exibe a guia **mapeamento de tipo** no SSMA, o plano de fundo é codificado por cor para mostrar quais mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
  
-   **Para mapear tipos de dados:**  
  
    Os procedimentos a seguir mostram como mapear os tipos de dados no nível de objeto do projeto, do banco de dados ou do:  
  
    1.  Para personalizar o mapeamento de tipo de dados para o projeto inteiro, abra a caixa de diálogo **configurações do projeto** . No menu ferramentas, selecione **configurações do projeto**.  
  
        No painel esquerdo, selecione **mapeamento de tipo**. O gráfico de mapeamento de tipo e os botões aparecem no painel direito.  
  
    2.  Para personalizar mapeamentos de tipo de dados no nível de tabela ou banco de dado, selecione o banco de dados ou a tabela no Gerenciador de metadados do MySQL. No Gerenciador de metadados do MySQL, selecione a pasta ou o objeto a ser personalizado.  
  
        No painel direito, clique em **mapeamento de tipo**.  
  
-   **Para adicionar um novo mapeamento, faça o seguinte:**  
  
    1.  No painel mapeamento de tipo, clique em **Adicionar** .  
  
    2.  Na caixa de diálogo novo mapeamento de tipo, em **tipo de origem**, selecione o tipo de dados do MySQL a ser mapeado.  
  
    3.  Se o tipo exigir um comprimento, especifique os comprimentos mínimo e máximo de dados para o mapeamento, marcando as caixas **de seleção de** e **para** e, em seguida, inserindo os valores.  
  
    4.  Isso permite que você personalize o mapeamento de dados para valores menores e maiores do mesmo tipo de dados. Em **tipo de destino**, selecione o tipo de dados SQL Server ou SQL Azure de destino.  
  
        1.  Alguns tipos exigem um comprimento de tipo de dados de destino. Se necessário, insira o novo comprimento dos dados na caixa **substituir por** e clique em **OK**.  
  
        2.  Alguns tipos exigem uma **escala**e **precisão** de tipo de dados de destino. Se necessário, insira a nova precisão e escala na caixa **substituir por** e clique em **OK**.  
  
-   **Para editar um mapeamento de tipo, faça o seguinte:**  
  
    1.  No painel mapeamento de tipo, clique em **Editar**.  
  
    2.  Na caixa de diálogo lista de mapeamento de tipos, em **tipo de origem**, selecione o tipo de dados do MySQL a ser mapeado.  
  
    3.  Se o tipo exigir um comprimento, especifique os comprimentos mínimo e máximo de dados para o mapeamento, marcando as caixas **de seleção de** e **para** e, em seguida, inserindo os valores.  
  
    Isso permite que você personalize o mapeamento de dados para valores menores e maiores do mesmo tipo de dados. Em **tipo de destino**, selecione o tipo de dados SQL Server ou SQL Azure de destino.  
  
    -  Alguns tipos exigem um comprimento de tipo de dados de destino. Se necessário, insira o novo comprimento dos dados na caixa **substituir por** e clique em **OK**.  
  
    -  Alguns tipos exigem uma **escala**e **precisão** de tipo de dados de destino. Se necessário, insira a nova precisão e escala na caixa **substituir por** e clique em **OK**.  
  
-   **Para remover um mapeamento de tipo de dados, faça o seguinte:**  
  
    1.  No painel mapeamento de tipo, selecione a linha na lista mapeamento de tipo que contém o mapeamento de tipo de dados que você deseja remover.  
  
    2.  Clique em **Remover**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [criar um relatório de avaliação](assessing-mysql-databases-for-conversion-mysqltosql.md) ou [converter objetos de banco de dados MySQL em SQL Server ou sintaxe de SQL Azure](converting-mysql-databases-mysqltosql.md). Se você criar um relatório, os objetos do MySQL serão convertidos automaticamente durante a avaliação.  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados MySQL para SQL Server-banco de MySQLToSql SQL do Azure &#40;&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

---
title: Mapeando tipos de dados do SybaseToSQL (ASE do Sybase e SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 79313d2344f6feb978a064f3fbd92e1f7bc7dce5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028896"
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Mapear ASE Sybase e tipos de dados do SQL Server (SybaseToSQL)
Os tipos de banco de dados do Sybase Adaptive Server Enterprise ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ase) diferem dos tipos de banco de dados ou SQL Azure. Ao converter objetos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do ase em objetos do ou SQL Azure, você deve especificar como mapear tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dado de ase para ou SQL Azure. Você pode aceitar os mapeamentos de tipo de dados padrão ou pode personalizar os mapeamentos, conforme mostrado nas seções a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto padrão de mapeamentos de tipo de dados. Para obter a lista de mapeamentos padrão, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
## <a name="type-mapping-inheritance"></a>Herança de mapeamento de tipo  
Você pode personalizar mapeamentos de tipo no nível de projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível superior, a menos que sejam substituídas em um nível inferior. Por exemplo, se você mapear **smallmoney** para **Money** no nível de projetos, todos os objetos no projeto usarão esse mapeamento, a menos que você personalize o mapeamento no nível de categoria de objeto ou de objeto.  
  
Quando você exibe a guia **mapeamento de tipo** no SSMA, o plano de fundo é codificado por cor para mostrar quais mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
O procedimento a seguir mostra como mapear tipos de dados no nível do projeto, do banco de dado ou do objeto.  
  
**Para mapear tipos de dados**  
  
1.  Para personalizar o mapeamento de tipo de dados para o projeto inteiro, abra a caixa de diálogo **configurações do projeto** :  
  
    1.  No menu **ferramentas** , selecione **configurações do projeto**.  
  
    2.  No painel esquerdo, selecione **mapeamento de tipo**.  
  
        O gráfico de mapeamento de tipo e os botões aparecem no painel direito.  
  
    Ou, para personalizar o mapeamento de tipo de dados no nível de banco de dado, tabela, exibição ou procedimento armazenado, selecione o banco de dados, a categoria de objeto ou o objeto no Gerenciador de metadados do Sybase:  
  
    1.  No Gerenciador de metadados do Sybase, selecione a pasta ou o objeto que você deseja personalizar.  
  
    2.  No painel direito, clique na guia **mapeamento de tipo** .  
  
2.  Para adicionar um novo mapeamento, faça o seguinte:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Em **tipo de origem**, selecione o tipo de dados do ase a ser mapeado.  
  
    3.  Se o tipo exigir um comprimento, especifique o comprimento mínimo dos dados para o mapeamento na caixa **de** e especifique o comprimento máximo dos dados para o mapeamento na caixa **para** .  
  
        Isso permite que você personalize o mapeamento de dados para valores menores e maiores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados de destino ou SQL Azure.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento dos dados na caixa **substituir por** .  
  
    5.  Clique em **OK**.  
  
3.  Para editar um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  Clique em **Editar**.  
  
    2.  Em **tipo de origem**, selecione o tipo de dados do ase a ser mapeado.  
  
    3.  Se o tipo exigir um comprimento, especifique o comprimento mínimo dos dados para o mapeamento na caixa **de** e especifique o comprimento máximo dos dados para o mapeamento na caixa **para** .  
  
        Isso permite que você personalize o mapeamento de dados para valores menores e maiores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados de destino ou SQL Azure.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento dos dados na caixa **substituir por** e clique em **OK**.  
  
4.  Para remover um mapeamento de tipo de dados personalizado, faça o seguinte:  
  
    1.  Selecione a linha na lista mapeamento de tipo que contém o mapeamento de tipo de dados que você deseja remover.  
  
    2.  Clique em **Remover**.  
  
        Não é possível remover mapeamentos herdados. No entanto, os mapeamentos herdados são substituídos por mapeamentos personalizados em um objeto ou categoria de objeto específico.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa do processo de migração é [criar um relatório de avaliação](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) ou [converter objetos de banco de dados de ase do Sybase para SQL Server ou SQL Azure sintaxe](converting-sybase-ase-database-objects-sybasetosql.md). Se você criar um relatório de avaliação, os objetos do Sybase ASE serão convertidos automaticamente durante a avaliação.  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

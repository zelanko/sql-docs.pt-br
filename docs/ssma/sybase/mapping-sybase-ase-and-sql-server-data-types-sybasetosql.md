---
title: Mapeamento Sybase ASE e tipos de dados do SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6952149829845872a78d5732671c1f9f9cd6a323
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Mapeamento Sybase ASE e tipos de dados do SQL Server (SybaseToSQL)
Os tipos de banco de dados do Sybase Adaptive Server Enterprise (ASE) variam de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tipos de banco de dados do SQL Azure. Ao converter objetos de banco de dados ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure, você deve especificar como mapear tipos de dados do ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você pode aceitar os mapeamentos de tipo de dados padrão, ou você pode personalizar os mapeamentos conforme mostrado nas seções a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto de mapeamentos de tipo de dados padrão. Para obter a lista de mapeamentos padrão, consulte [configurações de projeto &#40; Mapeamento de tipo de &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de mapeamento de herança  
Você pode personalizar mapeamentos de tipo no nível de projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível mais alto, a menos que substituída em um nível inferior. Por exemplo, se você mapear **smallmoney** para **money** no nível de projetos, todos os objetos no projeto usará esse mapeamento, a menos que você personalizar o mapeamento no nível de categoria de objeto ou no nível de objeto.  
  
Quando você exibe o **mapeamento de tipo** guia SSMA, o plano de fundo é codificadas por cor para mostrar os mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
O procedimento a seguir mostra como mapear tipos de dados no projeto, no banco de dados ou no nível de objeto.  
  
**Para mapear tipos de dados**  
  
1.  Para personalizar o mapeamento de tipo de dados para o projeto inteiro, abra o **configurações de projeto** caixa de diálogo:  
  
    1.  Sobre o **ferramentas** menu, selecione **configurações de projeto**.  
  
    2.  No painel esquerdo, selecione **mapeamento de tipo**.  
  
        Os botões e o gráfico de mapeamento de tipo aparecem no painel direito.  
  
    Ou, para personalizar o tipo de dados de mapeamento no banco de dados, tabela, exibição ou nível de procedimento armazenado, selecione o banco de dados, a categoria de objeto ou o objeto no Gerenciador de metadados do Sybase:  
  
    1.  No Gerenciador de metadados do Sybase, selecione a pasta ou o objeto que você deseja personalizar.  
  
    2.  No painel direito, clique no **mapeamento de tipo** guia.  
  
2.  Para adicionar um novo mapeamento, faça o seguinte:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Em **tipo de fonte**, selecione o tipo de dados ASE para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique o comprimento mínimo de dados para o mapeamento no **de** caixa e especifique o comprimento máximo dos dados para o mapeamento no **para** caixa.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tipo de dados do SQL Azure.  
  
        Alguns tipos de exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento de dados no **substitua** caixa.  
  
    5.  Clique em **OK**.  
  
3.  Para editar um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  Clique em **Editar**.  
  
    2.  Em **tipo de fonte**, selecione o tipo de dados ASE para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique o comprimento mínimo de dados para o mapeamento no **de** caixa e especifique o comprimento máximo dos dados para o mapeamento no **para** caixa.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tipo de dados do SQL Azure.  
  
        Alguns tipos de exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento de dados no **substitua** caixa e, em seguida, clique em **Okey**.  
  
4.  Para remover um mapeamento de tipo de dados personalizados, faça o seguinte:  
  
    1.  Selecione a linha na lista de mapeamento de tipo que contém o mapeamento de tipo de dados que deseja remover.  
  
    2.  Clique em **Remover**.  
  
        Você não pode remover mapeamentos herdados. No entanto, os mapeamentos herdados são substituídos pelas mapeamentos personalizados em um objeto específico ou a categoria de objeto.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa no processo de migração é como [criar um relatório de avaliação](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) ou [objetos de banco de dados Sybase ASE de converter a sintaxe do SQL Server ou SQL Azure](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3). Se você criar um relatório de avaliação, os objetos do Sybase ASE são convertidos automaticamente durante a avaliação.  
  
## <a name="see-also"></a>Consulte também  
[Migrando Sybase ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

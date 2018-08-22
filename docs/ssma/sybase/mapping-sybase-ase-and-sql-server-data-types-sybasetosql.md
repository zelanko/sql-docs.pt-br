---
title: Mapear ASE Sybase e tipos de dados do SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9efd87a25802bd5610393beb4de0728807ea827d
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395020"
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Mapear ASE Sybase e tipos de dados do SQL Server (SybaseToSQL)
Os tipos de banco de dados do Sybase Adaptive Server Enterprise (ASE) variam de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tipos de banco de dados do SQL Azure. Quando você converte objetos de banco de dados ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do SQL Azure, você deve especificar como mapear tipos de dados do ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode aceitar os mapeamentos de tipo de dados padrão, ou você pode personalizar os mapeamentos conforme mostrado nas seções a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto padrão de mapeamentos de tipo de dados. Para obter a lista de mapeamentos padrão, consulte [configurações do projeto &#40;mapeamento de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de mapeamento de herança  
Você pode personalizar mapeamentos de tipo no nível do projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível mais alto, a menos que substituído em um nível inferior. Por exemplo, se você mapear **smallmoney** à **money** no nível de projetos, todos os objetos no projeto usará esse mapeamento, a menos que você personalize o mapeamento no nível de categoria de objeto ou no nível do objeto.  
  
Quando você exibe o **mapeamento de tipo** guia no SSMA, o plano de fundo é codificadas por cores para mostrar quais mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e, em branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
O procedimento a seguir mostra como mapear tipos de dados no projeto, no banco de dados ou no nível do objeto.  
  
**Para mapear tipos de dados**  
  
1.  Para personalizar o mapeamento de tipo de dados para todo o projeto, abra o **configurações do projeto** caixa de diálogo:  
  
    1.  Sobre o **ferramentas** menu, selecione **configurações do projeto**.  
  
    2.  No painel esquerdo, selecione **mapeamento de tipo**.  
  
        O gráfico de mapeamento de tipo e os botões aparecem no painel direito.  
  
    Ou, para personalizar o tipo de dados de mapeamento no banco de dados, tabela, exibição ou nível de procedimento armazenado, selecione o banco de dados, a categoria de objeto ou o objeto no Gerenciador de metadados do Sybase:  
  
    1.  No Gerenciador de metadados do Sybase, selecione a pasta ou o objeto que você deseja personalizar.  
  
    2.  No painel direito, clique no **mapeamento de tipo** guia.  
  
2.  Para adicionar um novo mapeamento, faça o seguinte:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Sob **tipo de fonte**, selecione o tipo de dados ASE para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique o comprimento mínimo de dados para o mapeamento no **partir** caixa e especifique o comprimento máximo dos dados para o mapeamento no **para** caixa.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Sob **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tipo de dados do SQL Azure.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o comprimento de dados novo na **substitua** caixa.  
  
    5.  Clique em **OK**.  
  
3.  Para editar um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  Clique em **Editar**.  
  
    2.  Sob **tipo de fonte**, selecione o tipo de dados ASE para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique o comprimento mínimo de dados para o mapeamento no **partir** caixa e especifique o comprimento máximo dos dados para o mapeamento no **para** caixa.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Sob **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tipo de dados do SQL Azure.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o comprimento de dados novo na **substitua** caixa e, em seguida, clique em **Okey**.  
  
4.  Para remover um mapeamento de tipo de dados personalizada, faça o seguinte:  
  
    1.  Selecione a linha na lista de mapeamento de tipo que contém o mapeamento de tipo de dados que deseja remover.  
  
    2.  Clique em **Remover**.  
  
        Você não pode remover mapeamentos herdados. No entanto, mapeamentos herdados são substituídos pelas mapeamentos personalizados em uma categoria de objeto ou um objeto específico.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa no processo de migração é para qualquer um dos [criar um relatório de avaliação](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) ou [objetos de banco de dados ASE do Sybase converter a sintaxe do SQL Server ou SQL Azure](converting-sybase-ase-database-objects-sybasetosql.md). Se você criar um relatório de avaliação, os objetos do Sybase ASE são convertidos automaticamente durante a avaliação.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

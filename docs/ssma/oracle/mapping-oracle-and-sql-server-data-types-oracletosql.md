---
title: Mapeamento de Oracle e tipos de dados do SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 400ed2a28e622ffb9493af7462e06f551a214a51
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Mapeamento de Oracle e tipos de dados do SQL Server (OracleToSQL)
Os tipos de banco de dados Oracle variam de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de banco de dados. Ao converter objetos de banco de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos, você deve especificar como mapear tipos de dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você pode aceitar os mapeamentos de tipo de dados padrão, ou você pode personalizar os mapeamentos conforme mostrado nas seções a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto de mapeamentos de tipo de dados padrão. Para obter a lista de mapeamentos padrão, consulte [configurações de projeto &#40; Mapeamento de tipo de &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de mapeamento de herança  
Você pode personalizar mapeamentos de tipo no nível de projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível mais alto, a menos que elas são substituídas em um nível inferior. Por exemplo, se você mapear **smallmoney** para **money** no nível de projeto, todos os objetos no projeto usará esse mapeamento, a menos que você personalize o mapeamento no nível do objeto ou categoria.  
  
Quando você exibe o **mapeamento de tipo** guia SSMA, o plano de fundo é codificadas por cor para mostrar os mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
O procedimento a seguir mostra como mapear tipos de dados no projeto, no banco de dados ou no nível de objeto:  
  
**Para mapear tipos de dados**  
  
1.  Para personalizar o mapeamento de tipo de dados para o projeto inteiro, abra o **configurações de projeto** caixa de diálogo:  
  
    1.  Sobre o **ferramentas** menu, selecione **configurações de projeto**.  
  
    2.  No painel esquerdo, selecione **mapeamento de tipo**.  
  
        Os botões e o gráfico de mapeamento de tipo aparecem no painel direito.  
  
    Ou, para personalizar o tipo de dados de mapeamento no banco de dados, tabela, exibição ou nível de procedimento armazenado, selecione o banco de dados, a categoria de objeto ou o objeto no Gerenciador de metadados do Oracle:  
  
    1.  No Gerenciador de metadados do Oracle, selecione a pasta ou o objeto para personalizar.  
  
    2.  No painel direito, clique no **mapeamento de tipo** guia.  
  
2.  Para adicionar um novo mapeamento, faça o seguinte:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Em **tipo de fonte**, selecione o tipo de dados Oracle para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique o comprimento mínimo de dados para o mapeamento no **de** caixa e o comprimento máximo dos dados no **para** caixa.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados.  
  
        Alguns tipos de exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento de dados no **substitua** caixa.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  Para modificar um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  Clique em **Editar**.  
  
    2.  Em **tipo de fonte**, selecione o tipo de dados Oracle para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique o comprimento mínimo de dados para o mapeamento no **de** caixa e o comprimento máximo dos dados no **para** caixa.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados.  
  
        Alguns tipos de exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento de dados no **substitua** caixa e, em seguida,[!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
4.  Para remover um mapeamento de tipo de dados personalizados, faça o seguinte:  
  
    1.  Selecione a linha na lista de mapeamento de tipo que contém o mapeamento de tipo de dados que deseja remover.  
  
    2.  Clique em **Remover**.  
  
        Você não pode remover mapeamentos herdados. No entanto, os mapeamentos herdados são substituídos pelas mapeamentos personalizados em um objeto específico ou a categoria de objeto.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa no processo de migração é como [criar um relatório de avaliação](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357) ou [converter objetos de banco de dados Oracle em sintaxe de SQL Server](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272). Se você criar um relatório de avaliação, objetos Oracle são automaticamente convertidos durante a avaliação.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Oracle para o SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  


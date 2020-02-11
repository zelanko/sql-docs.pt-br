---
title: Mapeando tipos de dados DB2 e SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e7e939a8-5e76-4509-beaf-5acd1cab505e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1e9baab08f4295b2c51fd942f6153cc9425dd958
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68141006"
---
# <a name="mapping-db2-and-sql-server-data-types-db2tosql"></a>Mapeando tipos de dados DB2 e SQL Server (DB2ToSQL)
Tipos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 são diferentes dos tipos de banco de dados. Ao converter objetos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 em objetos, você deve especificar como mapear tipos de dado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do DB2 para o. Você pode aceitar os mapeamentos de tipo de dados padrão ou pode personalizar os mapeamentos, conforme mostrado nas seções a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto padrão de mapeamentos de tipo de dados. Para obter a lista de mapeamentos padrão, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md).  
  
## <a name="type-mapping-inheritance"></a>Herança de mapeamento de tipo  
Você pode personalizar mapeamentos de tipo no nível de projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível superior, a menos que sejam substituídas em um nível inferior. Por exemplo, se você mapear **smallmoney** para **Money** no nível do projeto, todos os objetos no projeto usarão esse mapeamento, a menos que você personalize o mapeamento no nível do objeto ou da categoria.  
  
Quando você exibe a guia **mapeamento de tipo** no SSMA, o plano de fundo é codificado por cor para mostrar quais mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
O procedimento a seguir mostra como mapear tipos de dados no nível do projeto, do banco de dado ou do objeto:  
  
**Para mapear tipos de dados**  
  
1.  Para personalizar o mapeamento de tipo de dados para o projeto inteiro, abra a caixa de diálogo **configurações do projeto** :  
  
    1.  No menu **ferramentas** , selecione **configurações do projeto**.  
  
    2.  No painel esquerdo, selecione **mapeamento de tipo**.  
  
        O gráfico de mapeamento de tipo e os botões aparecem no painel direito.  
  
    Ou, para personalizar o mapeamento de tipo de dados no nível de banco de dado, tabela, exibição ou procedimento armazenado, selecione o banco de dados, a categoria de objeto ou o objeto no Gerenciador de metadados do DB2:  
  
    1.  No Gerenciador de metadados do DB2, selecione a pasta ou o objeto a ser personalizado.  
  
    2.  No painel direito, clique na guia **mapeamento de tipo** .  
  
2.  Para adicionar um novo mapeamento, faça o seguinte:  
  
    1.  Clique em **Adicionar**.  
  
    2.  Em **tipo de origem**, selecione o tipo de dados DB2 a ser mapeado.  
  
    3.  Se o tipo exigir um comprimento, especifique o comprimento mínimo dos dados para o mapeamento na caixa **de** e o comprimento máximo dos dados na caixa **para** .  
  
        Isso permite que você personalize o mapeamento de dados para valores menores e maiores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados de destino.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento dos dados na caixa **substituir por** .  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Para modificar um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  Clique em **Editar**.  
  
    2.  Em **tipo de origem**, selecione o tipo de dados DB2 a ser mapeado.  
  
    3.  Se o tipo exigir um comprimento, especifique o comprimento mínimo dos dados para o mapeamento na caixa **de** e o comprimento máximo dos dados na caixa **para** .  
  
        Isso permite que você personalize o mapeamento de dados para valores menores e maiores do mesmo tipo de dados.  
  
    4.  Em **tipo de destino**, selecione o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados de destino.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o novo comprimento dos dados na caixa **substituir por** e, em seguida,[!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Para remover um mapeamento de tipo de dados personalizado, faça o seguinte:  
  
    1.  Selecione a linha na lista mapeamento de tipo que contém o mapeamento de tipo de dados que você deseja remover.  
  
    2.  Clique em **Remover**.  
  
        Não é possível remover mapeamentos herdados. No entanto, os mapeamentos herdados são substituídos por mapeamentos personalizados em um objeto ou categoria de objeto específico.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa do processo de migração é fazer o [relatório de avaliação &#40;DB2ToSQL&#41;](../../ssma/db2/assessment-report-db2tosql.md) ou [converter os esquemas do DB2 &#40;o DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md). Se você criar um relatório de avaliação, os objetos DB2 serão convertidos automaticamente durante a avaliação.  
  
## <a name="see-also"></a>Consulte Também  
[Migrar bancos de dados DB2 para SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

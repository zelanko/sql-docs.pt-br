---
title: Especificando definições de configuração para implantação de solução | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f711dc12ed5014dbc397e5a72f97f55350da7d38
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="deployment-script-files---solution-deployment-config-settings"></a>Arquivos de Script de implantação - definições de configuração de implantação de solução
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação do lê a partição e a função de opções de implantação que você usa no script de implantação do \< *nome do projeto*>. configsettings. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]cria esse arquivo quando você cria o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa as definições de configuração do projeto atual para criar o \< *nome do projeto*>. configsettings.  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a>Revisando parâmetros de configuração para implantação  
 A seguir estão as configurações armazenadas no \< *nome do projeto*>. configsettings:  
  
-   **Cadeias de Conexão de Fonte de Dados** São cadeias de caracteres de conexão para cada fonte de dados baseada nos valores especificados do projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . A ID de usuário e senha são sempre removidas da cadeia de caracteres de conexão antes da cadeia restante ser armazenada nesse arquivo. Porém, se o Assistente para Implantação estiver fazendo a implantação diretamente em uma instância do Analysis Services, você poderá adicionar as informações adequadas de ID de usuário e senha ao assistente para habilitar um processamento bem-sucedido do banco de dados de desenvolvimento. Essas informações de conexão não serão armazenadas no próprio script de implantação se alguma for salva pelo Assistente para Implantação.  
  
-   **Contas de representação** Esta configuração especifica o nome de usuário que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa para executar instruções em cada fonte de dados. Se nenhuma conta de representação for especificada, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará sua conta de logon para executar instruções. Se a conta de logon do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] receber permissões diretamente na fonte de dados, todos os administradores de banco de dados em todos os bancos de dados na instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] terão acesso à fonte de dados pela conta de logon. Se uma conta e senha do usuário forem especificadas, essas informações sempre serão removidas antes de as informações de representação serem armazenadas nesse arquivo. Porém, se o Assistente para Implantação estiver fazendo a implantação diretamente em uma instância do Analysis Services, você poderá adicionar as informações adequadas de ID de usuário e senha ao assistente para habilitar um processamento bem-sucedido do banco de dados de desenvolvimento. Essas informações de representação não serão armazenadas no próprio script de implantação se alguma for salva pelo Assistente para Implantação.  
  
-   **Arquivos de log de erros de chave** Essa configuração especifica o nome e o caminho do arquivo de log de erros de chave para cada cubo, grupo de medidas, partição e dimensão do banco de dados.  
  
-   **Locais de armazenamento** Essa configuração especifica o local de armazenamento para cada cubo, grupo de medidas e partição do banco de dados. Se nenhum valor for fornecido para um objeto, o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará o local padrão do objeto. Por exemplo, as partições usam o local para o grupo de medidas, os grupos de medidas usam o local para o cubo e os cubos usam o local padrão para objetos na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O local de armazenamento pode ser um local ou um caminho UNC (Convenção Universal de Nomenclatura).  
  
-   **Servidor de relatório** Esta configuração especifica o servidor de relatório e o local da pasta para cada ação de relatório definida em cada cubo no banco de dados.  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a>Modificando os parâmetros de configuração para implantação  
 Em alguns casos, talvez seja necessário implantar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto usando os parâmetros de configuração diferentes das armazenadas no \< *nome do projeto*>. configsettings. Por exemplo, convém alterar a cadeia de caracteres para uma ou mais fontes de dados ou especificar locais de armazenamento para partições ou grupos de medidas específicos.  
  
 Para modificar a implantação de partições e funções em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto, você deve alterar essas informações dentro de \< *nome do projeto*>. configsettings, conforme descrito no procedimento a seguir. Você não pode alterar as configurações de partição e de funções dentro do projeto porque o  *\<nome do projeto >* **páginas de propriedades** da caixa de diálogo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] não exibe essas opções.  
  
> [!NOTE]  
>  Os parâmetros de configuração podem se aplicar a todos os objetos ou só aos objetos recentemente criados. Aplique os parâmetros de configuração a objetos recém-criados apenas quando estiver implantando objetos adicionais em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anteriormente implantado e não quiser substituir os objetos existentes. Para especificar se as definições de configuração se aplicam a todos os objetos ou só aos recém-criados, defina essa opção \< *nome do projeto*>. deploymentoptions. Para obter mais informações, consulte [Especificando opções de implantação de função e de partição](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md).  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a>Para alterar os parâmetros de configuração depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interativamente, e na página **Parâmetros de Configuração** , especifique o parâmetro de configuração para os objetos que estão sendo implantados.  
  
     — ou —  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para executar em modo de arquivo de resposta. Para obter mais informações sobre o modo de arquivo de resposta, consulte [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     — ou —  
  
-   Modificar o \< *nome do projeto*>. configsettings usando qualquer editor de texto.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar o destino de instalação](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Especificando opções de implantação de função e de partição](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificando opções de processamento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  

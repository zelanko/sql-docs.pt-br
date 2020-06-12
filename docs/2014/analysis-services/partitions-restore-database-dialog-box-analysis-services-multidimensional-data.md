---
title: Partições (caixa de diálogo Restore Database) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.partitions.f1
ms.assetid: 1ad4dde5-4651-4069-875c-7ab73cd8b4f4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 489076bed7238f9367eeb8a353da358239673edb
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84540718"
---
# <a name="partitions-restore-database-dialog-box-analysis-services---multidimensional-data"></a>Partições (caixa de diálogo Restaurar Banco de Dados) (Analysis Services - Dados multidimensionais)
  Use a página **Partições** da caixa de diálogo **Restaurar Banco de Dados** em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para especificar o local de restauração de partições locais e para especificar se deseja restaurar partições remotas e arquivos de backup remotos para uso ao restaurar partições remotas.  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de restauração deve ter permissão para ler no local de backup especificado para cada arquivo. Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que não esteja instalado no servidor, o usuário também deve ser membro da função de servidor dessa instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para substituir um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , o usuário deve ter uma das seguintes funções: membro da função de servidor da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle Total (Administrador) no banco de dados a ser restaurado.  
  
> [!NOTE]  
>  Após restaurar um banco de dados existente, o usuário que o restaurou poderá perder o acesso ao banco de dados restaurado. Essa perda de acesso pode ocorrer se, no momento da execução do backup, o usuário não for membro da função de servidor, nem membro da função de banco de dados com permissões de Controle total (Administrador).  
  
 **Para exibir a página partições na caixa de diálogo Restaurar Banco de dados**  
  
-   No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na pasta **Bancos de Dados** de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou em um banco de dados em **Pesquisador de Objetos**, clique em **Restaurar**e, em **Selecionar uma página**, clique em **Partições**.  
  
## <a name="options"></a>Opções  
 **Script**  
 Cria um script de restauração baseado nas opções selecionadas na caixa de diálogo. O script de restauração é escrito na Linguagem de Scripts do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (ASSL).  
  
 Clicar no ícone **Script** envia o script de restauração a uma nova janela de consulta, por padrão.  
  
 Clicar na seta **Script** exibe um menu que permite escolher para onde enviar o script de restauração:  
  
-   Para uma nova janela de consulta (padrão).  
  
-   Para um arquivo.  
  
-   Para a área de transferência.  
  
-   Para um trabalho.  
  
 **Restaurar nos locais originais**  
 Selecione para restaurar em seus locais originais as partições locais contidas no arquivo de backup.  
  
 **Selecionar locais diferentes**  
 Selecione para especificar locais diferentes nos quais deseja restaurar as partições locais.  
  
> [!NOTE]  
>  Você só pode alterar a pasta de restauração de uma partição local se foi especificado para essa partição no cubo um local diferente do local padrão.  
  
 A grade a seguir, habilitada quando se seleciona esta opção, é usada para especificar uma pasta de restauração para cada partição local:  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**Simples**|Exibe o nome do cubo que contém a partição local.|  
|**MeasureGroup**|Exibe o nome do grupo de medidas que contém a partição local.|  
|**Particion**|Exibe o nome da partição local.|  
|**Tamanho (MB)**|Exibe o tamanho, em megabytes, da partição local.|  
|**Pasta original**|Exibe o nome da pasta original na qual a partição local foi armazenada.|  
|**Pasta de Restauração**|Digite o nome da pasta de restauração da partição local ou clique no botão de reticências (**...**) para exibir a caixa de diálogo **Procurar Pasta Remota** e selecione o caminho da pasta a ser usado. Para obter mais informações sobre a caixa de diálogo **Procurar Pasta Remota**, consulte [Caixa de diálogo Procurar Pasta Remota &#40;Analysis Services – Dados Multidimensionais&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md).|  
  
 **Restaurar partições remotas**  
 Selecione essa opção para restaurar partições remotas armazenadas em arquivos de backup remotos.  
  
> [!NOTE]  
>  Essa opção só será habilitada se o arquivo de backup contiver referências a partições remotas.  
  
 A grade a seguir, habilitada quando se seleciona esta opção, é usada para especificar uma pasta de restauração para cada partição local:  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**Servidor**|Exibe o nome da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra a partição remota.|  
|**Fonte de Dados**|Exibe o nome da fonte de dados no arquivo de backup que representa o banco de dados que contém a partição remota.|  
|**Arquivo de backup**|Digite o caminho completo e o nome de arquivo do arquivo de backup remoto a ser usado ou clique no botão de reticências (**...**) para exibir a caixa de diálogo **Localizar Arquivos de Banco de Dados** e selecione o caminho e o nome do arquivo de backup remoto a serem usados. Para obter mais informações sobre a caixa de diálogo **Localizar Arquivos de Banco de Dados**, consulte [Caixa de diálogo Localizar Arquivos de Banco de Dados &#40;Analysis Services – Dados Multidimensionais&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md).|  
|**...**|Clique para exibir a caixa de diálogo **Partições Remotas – Configurações Avançadas** e modificar opções avançadas, como a cadeia de conexão da fonte de dados, para restaurar a partição remota. Para obter mais informações sobre a caixa de diálogo **Partições Remotas – Configurações Avançadas**, consulte [Caixa de diálogo Partições Remotas – Configurações Avançadas &#40;Analysis Services – Dados Multidimensionais&#41;](remote-partitions-advanced-settings-dialog-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Restaurar Banco de dados &#40;Analysis Services-&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Geral &#40;caixa de diálogo Restaurar Banco de dados&#41; &#40;Analysis Services –&#41;multidimensional](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Backup e restauração de bancos de dados do Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  

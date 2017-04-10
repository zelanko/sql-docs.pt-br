---
title: "Backup e restaura&#231;&#227;o de bancos de dados do Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.ssmsimbi.Restore.f1"
  - "sql13.asvs.ssmsimbi.Backup.f1"
helpviewer_keywords: 
  - "fazendo backup de bancos de dados [Analysis Services]"
  - "criptografia [Analysis Services]"
  - "bancos de dados [Analysis Services], restaurando"
  - "criptografia [Analysis Services]"
  - "bancos de dados [Analysis Services], fazendo backup"
  - "restaurando bancos de dados [Analysis Services]"
  - "recuperação [Analysis Services]"
ms.assetid: 947eebd2-3622-479e-8aa6-57c11836e4ec
caps.latest.revision: 54
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 54
---
# Backup e restaura&#231;&#227;o de bancos de dados do Analysis Services
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui backup e restauração de forma que você possa recuperar um banco de dados e seus objetos de um ponto específico no tempo. Backup e restauração também é uma técnica válida por migrar bancos de dados para servidores atualizados, mover bancos de dados entre servidores ou implantar um banco de dados para um servidor de produção. Para fins de recuperação de dados, se você ainda não tem um plano de backup e seus dados são valiosos, deve criar e implementar um plano o mais breve possível.  
  
 Os comandos de backup e restauração são executados em um banco de dados implantado do Analysis Services. Para seus projetos e soluções no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você deve usar o controle do código-fonte para garantir que possa recuperar versões específicas de seus arquivos de origem e, então, criar um plano de recuperação de dados para o repositório do sistema de controle do código-fonte que você estiver usando.  
  
 Para um backup completo que inclua dados de origem, você tem que fazer o backup do banco de dados que contém os detalhes dos dados. Especificamente, se você estiver usando o armazenamento de banco de dados ROLAP ou DirectQuery, os dados detalhados serão armazenados em um banco de dados relacional externo do SQL Server que é diferente do banco de dados do Analysis Services. Caso contrário, se todos os objetos forem de tabela ou multidimensionais, o backup do Analysis Services incluirá os metadados e os dados de origem.  
  
 Um benefício claro de automatizar o backup é que os instantâneos de dados sempre estarão tão atualizados quanto à frequência automatizada de backup especifica. Agendadores automatizados garantem o não esquecimento dos backups. A restauração de um banco de dados também pode ser automatizada e ser uma boa maneira de replicar dados, mas certifique-se de fazer o backup do arquivo da chave de criptografia na instância para a qual deseja fazer a replicação. O recurso de sincronização é dedicado à replicação de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , mas somente para os dados obsoletos. Todos os recursos mencionados aqui podem ser implementados pela interface do usuário, por meio de comandos XML/A ou executados programaticamente pelo AMO. Para obter mais informações sobre estratégias de backup, consulte [Backup Strategies with SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81888).  
  
 Este tópico inclui as seguintes seções:  
  
-   [Preparando para backup](#bkmk_prep)  
  
-   [Fazendo backup de um banco de dados multidimensional ou de tabela](#bkmk_cube)  
  
-   [Restaurando um banco de dados do Analysis Services](#bkmk_restore)  
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
 Você deve ter permissões administrativas na instância do Analysis Services ou permissões de Controle completo (Administrador) no banco de dados do qual você está fazendo backup.  
  
 O local de restauração deve ser uma instância do Analysis Services que é da mesma versão ou de uma versão mais nova, como a instância da qual o backup foi feito. Embora você não possa restaurar um banco de dados de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para uma versão anterior do Analysis Services, é prática comum restaurar um banco de dados de versão anterior, como o SQL Server 2012, em uma instância mais recente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 O local de restauração deve ser o mesmo tipo de servidor. Os bancos de dados tabulares somente podem ser restaurados para um Analysis Services que esteja sendo executado em modo tabular. Os bancos de dados multidimensionais exigem uma instância que é executada em modo multidimensional.  
  
##  <a name="bkmk_prep"></a> Preparando para backup  
 Use a lista de verificação a seguir para preparar para o backup:  
  
-   Verifique o local em que o arquivo de backup será armazenado. Se você estiver usando um local remoto, deverá especificá-lo como uma pasta UNC. Verifique se você pode acessar o caminho UNC.  
  
-   Verifique as permissões na pasta para verificar se a conta de serviço do Analysis Services tem permissões de leitura e gravação na pasta.  
  
-   Verifique se há espaço em disco suficiente no servidor de destino.  
  
-   Verifique se há arquivos existentes do mesmo nome. Se já existir um arquivo com o mesmo nome, o backup falhará, a menos que você especifique opções para substituir o arquivo.  
  
##  <a name="bkmk_cube"></a> Fazendo backup de um banco de dados multidimensional ou de tabela  
 Os administradores podem fazer backup de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um único arquivo de backup (.abf) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], seja qual for o tamanho do banco de dados. Para obter instruções passo a passo, consulte [Como fazer backup de um banco de dados do Analysis Services (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Backup_an_Analysis_Services_Database.html) e [Automatizar o backup de um banco de dados do Analysis Services (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Automate_Backup_of_Analysis_Services_Database.html).  
  
> [!NOTE]  
>  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], usado para carregar e consultar modelos de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um ambiente do SharePoint, carrega seus modelos de bancos de dados de conteúdo do SharePoint. Esses bancos de dados de conteúdo são relacionais e executados no mecanismo de banco de dados relacional do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Como tal, não há backup do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e estratégia de restauração para modelos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se você tiver um plano de recuperação de desastres em vigor para o conteúdo do SharePoint, esse plano abrangerá os modelos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] armazenados nos bancos de dados de conteúdo.  
  
 **Partições remotas**  
  
 Se o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contiver partições remotas, elas também deverão ser submetidas a backup. Quando você fizer backup de um banco de dados com partições remotas, todas as partições remotas em cada servidor remoto terão seu backup feito em um único arquivo, em cada um desses servidores remotos respectivamente. Então, se você quiser criar esses backups remotos fora de seus respectivos computadores host, terá que copiar esses arquivos manualmente nas áreas de armazenamento designadas.  
  
 **Conteúdo de um arquivo de backup**  
  
 Fazer o backup de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gera um arquivo de backup cujo conteúdo varia em função do modo de armazenamento usado pelos objetos de banco de dados. Essa diferença no conteúdo do backup resulta do fato de que cada modo de armazenamento na realidade armazena um conjunto diferente de informações dentro de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por exemplo, as partições e dimensões de HOLAP (OLAP híbrido) multidimensionais armazenam agregações e metadados no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], enquanto as partições e dimensões de ROLAP (OLAP relacional) só armazenam metadados no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Como o conteúdo real de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] varia com base no modo de armazenamento de cada partição, o conteúdo do arquivo de backup também varia. A tabela a seguir associa o conteúdo do arquivo de backup ao modo de armazenamento usado pelos objetos.  
  
|Modo de armazenamento|Conteúdo de arquivo de backup|  
|------------------|-----------------------------|  
|Partições e dimensões multidimensionais MOLAP|Metadados, dados de origem e agregações|  
|Partições e dimensões multidimensionais HOLAP|Metadados e agregações|  
|Partições e dimensões multidimensionais ROLAP|Metadados|  
|Modelos em memória de tabela|Metadados e dados de origem|  
|Modelos DirectQuery de tabela|Somente metadados|  
  
> [!NOTE]  
>  Fazer backup de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não faz com que seja feito backup em qualquer das fontes de dados subjacentes, como um banco de dados relacional. Só é feito backup do conteúdo do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Quando você fizer backup de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , poderá escolher as seguintes opções:  
  
-   Compactar ou não todos os backups de banco de dados. O padrão é compactar os backups.  
  
-   Criptografar ou não o conteúdo dos arquivos de backup e solicitar uma senha antes de o arquivo ser descriptografado e restaurado. Por padrão, dados com backup não são criptografados.  
  
    > [!IMPORTANT]  
    >  Para cada arquivo de backup, o usuário que executar o comando de backup deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: membro de uma função de servidor para a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados cujo backup será feito.  
  
 Para obter mais informações sobre como fazer backup de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Opções de backup](../../analysis-services/multidimensional-models/backup-options.md).  
  
##  <a name="bkmk_restore"></a> Restaurando um banco de dados do Analysis Services  
 Os administradores podem restaurar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de um ou mais arquivos de backup.  
  
> [!NOTE]  
>  Se um arquivo de backup estiver criptografado, forneça a senha especificada durante o backup antes de usar esse arquivo para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Durante a restauração, as seguintes opções estão disponíveis:  
  
-   Você pode restaurar o banco de dados usando o nome do banco de dados original ou especificar um novo nome para ele.  
  
-   Você pode substituir um banco de dados existente. Se você escolher substituir o banco de dados, especifique expressamente que deseja substituir o banco de dados existente.  
  
-   Você pode escolher restaurar a informação de segurança já existente ou ignorar as informações de associação de segurança.  
  
-   Você pode optar que o comando de restauração altere a pasta de restauração de cada partição que estiver sendo restaurada. As partições locais poderão ser restauradas para qualquer local de pasta que seja local à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para a qual o banco de dados está sendo restaurado. As partições remotas podem ser restauradas para qualquer pasta em qualquer servidor, diferente do servidor local; as partições remotas não podem se tornar locais.  
  
    > [!IMPORTANT]  
    >  Para cada arquivo de backup, o usuário que executar o comando de restauração deve ter permissão para ler no local de backup especificado para cada arquivo. Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que não esteja instalado no servidor, o usuário também deve ser membro da função de servidor dessa instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para substituir um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o usuário deve ter uma das seguintes funções: membro da função de servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle Total (Administrador) no banco de dados a ser restaurado.  
  
    > [!NOTE]  
    >  Após restaurar um banco de dados existente, o usuário que o restaurou poderá perder o acesso ao banco de dados restaurado. Essa perda de acesso pode ocorrer se, no momento da execução do backup, o usuário não for membro da função de servidor, nem membro da função de banco de dados com permissões de Controle total (Administrador).  
  
 Para obter mais informações sobre como restaurar um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Opções de restauração](../../analysis-services/multidimensional-models/restore-options.md).  
  
## Consulte também  
 [Fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)   
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)  
  
  
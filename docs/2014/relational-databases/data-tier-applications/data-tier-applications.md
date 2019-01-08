---
title: Aplicativos da camada de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- designing DACs
- How to [DAC]
- data-tier application [SQL Server], designing
- wizard [DAC]
ms.assetid: a04a2aba-d07a-4423-ab8a-0a31658f6317
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b9731a25633b5bc127039ae81a31df8c69bb8ccb
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540118"
---
# <a name="data-tier-applications"></a>Aplicativos da camada de Dados
  Um aplicativo da camada de dados (DAC) é uma entidade de gerenciamento de banco de dados lógico que define todos os objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], assim como tabelas, exibições e objetos de instância, inclusive logons, associados do banco de dados do usuário. Um DAC é uma unidade autossuficiente de implantação de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite que desenvolvedores da camada de dados e administradores de banco de dados empacotem objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um artefato portátil chamado pacote de DAC, também conhecido como DACPAC.  
  
 Um BACPAC é um artefato relacionado que encapsula o esquema de banco de dados e também os dados armazenados no banco de dados.  
  
## <a name="benefits-of-data-tier-applications"></a>Benefícios de aplicativos da camada de dados  
 O ciclo de vida da maioria dos aplicativos de banco de dados envolve desenvolvedores e DBAs compartilhando e trocando scripts e notas de integração ad hoc para atualização de aplicativo e atividades de manutenção. Embora isto seja aceitável para um número pequeno de bancos de dados, torna-se rapidamente impossível de evoluir se os bancos de dados crescerem em número, tamanho e complexidade.  
  
 Um DAC é uma ferramenta de produtividade e de gerenciamento de ciclo de vida de banco de dados que permite o desenvolvimento de banco de dados declarativo para simplificar a implantação e o gerenciamento. Um desenvolvedor pode criar um banco de dados no projeto de banco de dados do Ferramentas de Dados do SQL Server e, em seguida, compilar o banco de dados em um DACPAC para entregar para um DBA. O DBA pode implantar o DAC usando o SQL Server Management Studio para um teste ou instância de produção do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Como alternativa, o DBA pode usar o DACPAC para atualizar um banco de dados previamente implantado usando o SQL Server Management Studio. Para concluir o ciclo de vida, o DBA pode extrair o banco de dados em um DACPAC e entregá-lo a um desenvolvedor para refletir ajustes de teste ou produção, ou para habilitar alterações adicionais de design de banco de dados em relação a alterações no aplicativo.  
  
 A vantagem de uma implantação orientada por DAC em relação a um exercício orientado por script é que a ferramenta ajuda o DBA a identificar e validar comportamentos de bancos de dados de origem e destino diferentes. Durante atualizações, a ferramenta avisa o DBA se a atualização pode causar perda de dados, e também fornece um plano de atualização. O DBA pode avaliar o plano e, em seguida, utilizar a ferramenta para continuar com a atualização.  
  
 Os DACs também dão suporte a controle de versão para ajudar o desenvolvedor e o DBA a manter e gerenciar a linhagem de banco de dados em todo o seu ciclo de vida.  
  
## <a name="dac-concepts"></a>Conceitos de DAC  
 Um DAC simplifica o desenvolvimento, a implantação e o gerenciamento dos elementos da camada de dados que oferecem suporte a um aplicativo.  
  
-   Um DAC (aplicativo da camada de dados) é uma entidade lógica de gerenciamento de banco de dados que define todos os objetos SQL Server como tabelas, exibições e objetos de instância, associados a um banco de dados de usuário. Se uma unidade autossuficiente de implantação de banco de dados do SQL Server que permite que desenvolvedores da camada de dados e DBAs empacotem objetos SQL Server em um artefato portátil chamado pacote de DAC, ou arquivo .dacpac.  
  
-   Para que um banco de dados do SQL Server seja tratado como um DAC, ele deverá ser registrado ou explicitamente por uma operação de usuário ou implicitamente por uma das operações de DAC. Quando um banco de dados é registrado, a versão do DAC e outras propriedades são registradas como parte dos metadados do banco de dados. De maneira recíproca, um banco de dados também pode ter o registro cancelado e ter suas propriedades do DAC removidas.  
  
-   Em geral, as ferramentas do DAC são capazes de ler arquivos do DACPAC gerados por ferramentas de DAC de versões anteriores do SQL Server e também podem implantar o DACPAC em versões anteriores do SQL Server. No entanto, as ferramentas de DAC de versões anteriores não podem ler arquivos DACPAC gerados por ferramentas do DAC de versões posteriores. Especificamente:  
  
    -   As operações do DAC foram introduzidas no SQL Server 2008 R2. Além de bancos de dados do SQL Server 2008 R2, as ferramentas dão suporte à geração de arquivos DACPAC de bancos de dados do SQL Server 2008, do SQL Server 2005 e do SQL Server 2000.  
  
    -   Além de bancos de dados de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , as ferramentas enviadas com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] podem ler arquivos DACPAC gerados por ferramentas de DAC enviadas com o SQL Server 2008 R2 ou SQL Server 2012. Isto inclui bancos de dados do SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 e SQL Server 2005, mas não SQL Server 2000.  
  
    -   As ferramentas de DAC do SQL Server 2008 R2 não podem ler arquivos DACPAC gerados por ferramentas do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Um DACPAC é um arquivo do Windows com uma extensão .dacpac. O arquivo dá suporte a um formato aberto que consiste em várias seções de XML que representam detalhes da origem de DACPAC, os objetos no banco de dados e outras características. Um usuário avançado pode descompactar o arquivo usando o utilitário DacUnpack.exe que é enviado com o produto para inspecionar cada seção mais de perto.  
  
-   O usuário deve ser membro da função dbmanager ou ter permissões CREATE DATABASE atribuídas para criar um banco de dados, incluindo criar um banco de dados implantando um pacote de DAC. O usuário deve ser um membro da função dbmanager ou ter permissões DROP DATABASE atribuídas para remover um banco de dados.  
  
## <a name="dac-tools"></a>Ferramentas de DAC  
 Um DACPAC pode ser usado diretamente por várias ferramentas que são enviadas com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Estas ferramentas tratam os requisitos de diferentes personas de usuário usando um DACPAC como a unidade de interoperabilidade.  
  
-   Desenvolvedor de aplicativo  
  
    -   Um desenvolvedor de banco de dados pode usar um projeto de banco de dados do SQL Server Data Tools para criar um banco de dados. Uma compilação bem-sucedida deste projeto resulta na geração de um DACPAC contido em um arquivo .dacpac.  
  
    -   Além disso, o desenvolvedor pode importar um DACPAC em um projeto de banco de dados e continuar criando o banco de dados.  
  
    -   O SQL Server Data Tools também oferece suporte a um Local DB para desenvolvimento de aplicativo de banco de dados desconectado do lado do cliente. O desenvolvedor pode fazer um instantâneo deste banco de dados local para criar o DACPAC contido em um arquivo .dacpac.  
  
    -   Independentemente, o desenvolvedor pode publicar um projeto de banco de dados diretamente em um banco de dados sem precisar gerar um DACPAC. A operação de publicar segue comportamento semelhante à operação de implantar de outras ferramentas.  
  
-   Administrador de banco de dados  
  
    -   Um DBA pode usar o SQL Server Management Studio para extrair um DACPAC de um banco de dados existente e também executar outras operações de DAC.  
  
    -   Além disso, o DBA para um banco de dados do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] pode usar o Portal de Gerenciamento para SQL Azure para operações de DAC.  
  
-   Fornecedores de software independentes  
  
    -   Serviços de hospedagem e outros produtos de gerenciamento de dados para o SQL Server podem usar a API do DACFx para operações de DAC.  
  
-   Administrador de TI  
  
    -   Integradores de sistemas de TI e administradores podem usar a ferramenta de linha de comando do SqlPackage.exe para operações de DAC.  
  
## <a name="dac-operations"></a>Operações DAC  
 O DAC oferece suporte às seguintes operações:  
  
-   **EXTRACT** – o usuário pode extrair um banco de dados em um DACPAC.  
  
-   **DEPLOY** – o usuário pode implantar um DACPAC em um servidor de host. Quando a implantação é feita de uma ferramenta de gerenciabilidade como SQL Server Management Studio ou o Portal de Gerenciamento para SQL Azure, o banco de dados resultante no servidor do host é registrado implicitamente como um aplicativo da camada de dados.  
  
-   **REGISTER** – o usuário pode registrar um banco de dados como um aplicativo da camada de dados.  
  
-   **UNREGISTER** – um banco de dados previamente registrado como um DAC pode ter o registro cancelado.  
  
-   **UPGRADE** – um banco de dados pode ser atualizado usando um DACPAC. A atualização tem suporte mesmo em bancos de dados que não estejam previamente registrados como aplicativos de camada de dados, mas, como uma consequência da atualização, o banco de dados será registrado implicitamente.  
  
## <a name="backup-package-bacpac"></a>Pacote de backup (.bacpac)  
 Um BACPAC é um artefato que encapsula o esquema de banco de dados e também os dados armazenados no banco de dados. O BACPAC é um arquivo do Windows com uma extensão .bacpac. Semelhante ao DACPAC, o formato de arquivo do BACPAC é aberto – o conteúdo de esquema do BACPAC é idêntico ao do DACPAC. Os dados são armazenados em formato JSON.  
  
 DACPAC e BACPAC são semelhantes, mas eles se destinam a cenários diferentes. Um DACPAC destina-se a capturar e implantar esquema, inclusive atualizar um banco de dados existente. Caso de uso primário para um DACPAC é implantar um esquema altamente definido para desenvolvimento, teste e, em seguida, ambientes de produção e o inverso: capturar o esquema de produção e aplicá-lo novamente para teste e ambientes de desenvolvimento.  
  
 Por outro lado, um BACPAC destina-se a capturar esquema e dados. Um BACPAC é o equivalente lógico de um backup de banco de dados e não pode ser usado para atualizar bancos de dados existentes. O caso de uso primário para um BACPAC é mover um banco de dados de um servidor para outro - ou de um servidor local para a nuvem - e arquivar um banco de dados existente em um formato aberto.  
  
 Um BACPAC dá suporte a duas operações principais:  
  
-   **EXPORT**– o usuário pode exportar o esquema e os dados de um banco de dados para um BACPAC.  
  
-   **IMPORT** – o usuário pode importar o esquema e os dados em um novo banco de dados no servidor de host.  
  
 Estes recursos têm suporte pelas ferramentas de gerenciamento de banco de dados: Server Management Studio, o Portal de gerenciamento para SQL Azure e a API DACFx.  
  
## <a name="permissions"></a>Permissões  
 Você deve ser membro da função `dbmanager` ou ter permissões `CREATE DATABASE` atribuídas para criar um banco de dados, incluindo criar um banco de dados implantando um pacote de DAC. Você deve ser um membro da função `dbmanager` ou ter permissões `DROP DATABASE` atribuídas para remover um banco de dados.  
  
## <a name="data-tier-application-tasks"></a>Tarefas do aplicativo da camada de dados  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como usar um arquivo de pacote de DAC para criar uma nova instância do DAC.|[Implantar um aplicativo da camada de dados](deploy-a-data-tier-application.md)|  
|Descreve como usar um novo arquivo do pacote de DAC para atualizar uma instância para uma nova versão do DAC.|[Atualizar um aplicativo da camada de dados](upgrade-a-data-tier-application.md)|  
|Descreve como remover uma instância do DAC. Você pode escolher também desanexar ou remover o banco de dados associado ou deixar o banco de dados intacto.|[Excluir um aplicativo da camada de dados](delete-a-data-tier-application.md)|  
|Descreve como exibir a integridade de DACs atualmente implantado usando o Utilitário do SQL Server.|[Monitorar aplicativos da camada de dados](data-tier-applications.md)|  
|Descreve como criar um arquivo .bacpac que contém um arquivo morto dos dados e metadados em um DAC.|[Exportar um aplicativo da camada de dados](export-a-data-tier-application.md)|  
|Descreve como usar um arquivo morto de DAC (.bacpac) para executar uma restauração lógica de um DAC ou para migrar o DAC para outra instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|[Importar um arquivo BACPAC para criar um novo banco de dados de usuário](import-a-bacpac-file-to-create-a-new-user-database.md)|  
|Descreve como importar um arquivo BACPAC para criar um novo banco de dados de usuário dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Extrair um DAC de um banco de dados](extract-a-dac-from-a-database.md)|  
|Descreve como elevar um banco de dados existente para ser uma instância do DAC. Uma definição de DAC é criada e armazenada nos bancos de dados do sistema.|[Registrar um banco de dados como um DAC](register-a-database-as-a-dac.md)|  
|Descreve como examinar o conteúdo de um pacote de DAC e as ações que uma atualização de DAC executará antes de usar o pacote em um sistema de produção.|[Validar um pacote de DAC](validate-a-dac-package.md)|  
|Descreve como colocar o conteúdo de um pacote de DAC em uma pasta onde um administrador de banco de dados pode analisar o que o DAC faz antes de implantá-lo em um servidor de produção.|[Desempacotar um pacote de DAC](unpack-a-dac-package.md)|  
|Descreve como usar um assistente para implantar um banco de dados existente. O assistente usa os DACs para executar a implantação.|[Implantar um banco de dados usando um DAC](deploy-a-database-by-using-a-dac.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao DAC para objetos e versões do SQL Server](dac-support-for-sql-server-objects-and-versions.md)  
  
  

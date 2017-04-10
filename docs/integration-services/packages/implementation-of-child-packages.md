---
title: "Implementa&#231;&#227;o de pacotes filho | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes filho"
ms.assetid: ab0c09d7-ce2e-487d-a1ed-a4b5adb6cc01
caps.latest.revision: 40
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Implementa&#231;&#227;o de pacotes filho
  Quando você implementa balanceamento de carga usando o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], os pacotes filho são instalados em outros servidores para aproveitar a CPU disponível ou o tempo do servidor. Para criar e executar os pacotes filho são necessárias as seguintes etapas:  
  
-   Criar os pacotes filho.  
  
-   Mover os pacotes para o servidor remoto.  
  
-   Criar um trabalho do SQL Server Agent no servidor remoto que contém uma etapa que executa o pacote filho.  
  
-   Testar e depurar o trabalho do SQL Server Agent e os pacotes filho.  
  
 Quando você cria pacotes filho, os pacotes não têm nenhuma limitação em sua criação e é possível inserir qualquer funcionalidade desejada. Entretanto, se o pacote acessar dados, será necessário verificar se o servidor que executa o pacote tem acesso aos dados.  
  
 Para identificar o pacote pai que executa pacotes filho, em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse no pacote no Gerenciador de Soluções e clique em **Pacote de Ponto de Entrada**.  
  
 Depois que os pacotes filho são criados, a próxima etapa é implantá-los nos servidores remotos.  
  
## Mover o pacote filho para uma instância remota  
 Há várias maneiras de mover os pacotes para outros servidores. Os dois métodos sugeridos são:  
  
-   Exportar os pacotes usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Implantar os pacotes compilando um utilitário de implantação para o projeto que contém os pacotes que você deseja implantar e, depois, executar o Assistente de Instalação de Pacotes para instalar os pacotes no sistema de arquivos ou em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
 Você precisa repetir a implantação em cada servidor remoto que desejar usar.  
  
## Criar trabalhos do SQL Server Agent  
 Depois que os pacotes filho forem implantados em vários servidores, crie um trabalho do SQL Server Agent em cada servidor que contém um pacote filho. O trabalho do SQL Server Agent possui uma etapa que executa o pacote filho quando o agente de trabalhos é chamado. Os trabalhos do SQL Server Agent não são trabalhos agendados; eles executam os pacotes filho somente quando são chamados pelo pacote pai. A notificação de êxito ou falha do trabalho no pacote pai reflete o sucesso ou a falha do trabalho do SQL Server Agent e se ele foi chamado com êxito, e não o êxito ou o fracasso do pacote filho ou se ele foi executado.  
  
## Depurar os trabalhos do SQL Server Agent e os pacotes filho  
 Você pode testar os trabalhos do SQL Server Agent e seus pacotes filho usando um dos seguintes métodos:  
  
-   Executar cada pacote filho no Designer SSIS clicando em **Depurar**  /  **Iniciar sem Depurar**.  
  
-   Executar o trabalho individual do SQL Server Agent no computador remoto usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]para garantir que o pacote seja executado.  
  
 Para obter informações sobre como resolver problemas de pacotes executados nos trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Um pacote SSIS não é executado quando você chama o pacote SSIS a partir de um trabalho do SQL Server Agent](http://support.microsoft.com/kb/918760) na Base de Dados de Conhecimento de Suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 O SQL Server Agent realiza verificações no acesso do subsistema para um proxy e fornece acesso ao proxy toda vez que a etapa do trabalho é executada.  
  
 Você pode criar um proxy no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## Tarefas relacionadas  
  
-   [Executar um pacote no servidor SSIS usando o SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  
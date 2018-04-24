---
title: Adquirir e configurar um servidor de carregamento - Parallel Data Warehouse | Microsoft Docs
description: Este artigo descreve como adquirir e configurar um servidor de carregamento como um sistema do Windows não seja de aplicação para o envio de cargas de dados para o Parallel Data Warehouse (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a796616ad76ba62ea4174cf22c1517c489305055
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>Adquirir e configurar um servidor de carregamento para Parallel Data Warehouse
Este artigo descreve como adquirir e configurar um servidor de carregamento como um sistema do Windows não seja de aplicação para o envio de cargas de dados para o Parallel Data Warehouse (PDW).  
  
## <a name="Basics"></a>Noções básicas  
O servidor de carregamento:  
  
-   Não precisa ser um único servidor. Você pode carregar simultaneamente vários servidores de carregamento.  
  
-   É fornecido e gerenciados pela sua equipe de TI. Talvez você já tenha um servidor ou servidores que podem ser usados para carregar dados no PDW.  
  
-   Está localizado em seu próprio rack não seja de aplicação e não pode ser colocado no dispositivo Analytics Platform System.  
  
-   Está conectado ao dispositivo por meio da rede InfiniBand de dispositivo ou pela Ethernet. Para obter desempenho, é recomendável usar InfiniBand.  
  
-   Está em seu próprio domínio de cliente, não o domínio de aplicativo. Não há nenhuma relação de confiança entre o domínio de cliente e o domínio de aplicativo.  
  
## <a name="Step1"></a>Etapa 1: Determinar requisitos de capacidade  
O sistema de carregamento pode ser projetado como um ou mais servidores de carregamento que executam carregamentos simultâneos. Cada servidor de carregamento não precisa ser dedicada somente para carregamento, desde que ele tratará os requisitos de armazenamento e o desempenho da carga de trabalho.  
  
Os requisitos de sistema para um servidor de carregamento quase que totalmente dependem de sua carga de trabalho. Use o [carregar planilha de planejamento de capacidade de servidor](loading-server-capacity-planning-worksheet.md) para ajudar a determinar seus requisitos de capacidade.  
  
## <a name="Step2"></a>Etapa 2: Adquirir o Sservidor  
Agora que você entender melhor os seus requisitos de capacidade, você pode planejar os servidores e os componentes de rede que você precisará comprar ou provisionar. Incorporar a seguinte lista de requisitos de seu plano de compra, compra seu servidor ou provisionar um servidor existente.  
  
### <a name="R"></a>Requisitos de software  
Sistemas operacionais com suporte:  
  
-   No Windows Server 2012 ou Windows Server 2012 R2. Esses sistemas operacionais exigem o adaptador de rede FDR.  
  
-   Windows Server 2008 R2. Neste sistema operacional requer que o adaptador de rede DDR.  
  
O servidor deve usar a localidade EN-US para usar a ferramenta de linha de comando ao carregar dwloader. dwloader não dá suporte a outras localidades.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Requisitos de rede para o Windows Server 2012 e Windows Server 2012 R2  
Embora não seja necessário para carregamento, InfiniBand é o tipo de conexão recomendado para servidores de carregamento. Para melhor desempenho, use o Windows Server 2012 ou Windows Server 2012 R2 e o adaptador de rede InfiniBand FDR para conectar o servidor de carregamento para a rede InfiniBand do dispositivo.  
  
Para preparar para uma conexão do Windows Server 2012 ou Windows Server 2012 R2 InfiniBand:  
  
1.  Planejar o servidor de rack aproximados o suficiente para o dispositivo para que você pode conectá-lo para o dispositivo alterna InfiniBand. Para saber mais sobre InfiniBand Mellanox tecnologias, consulte o white paper, [Introdução ao InfiniBand](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Compre um adaptador de rede de porta única ou dupla Mellanox ConnectX-3 FDR InfiniBand. Recomendamos que você comprar o adaptador de rede com duas portas para tolerância a falhas durante a transmissão de dados. Um adaptador de rede de duas portas é necessário para alta disponibilidade.  
  
3.  Compre 2 cabos FDR InfiniBand para uma placa de porta dupla ou 1 cabo FDR InfiniBand para uma placa de porta única. Os cabos FDR InfiniBand conectará o carregando o servidor à rede InfiniBand appliance. O comprimento de cabo depende da distância entre o servidor de carregamento e as opções do dispositivo InfiniBand, acordo com seu ambiente.  
  
## <a name="Step3"></a>Etapa 3: Conectar o servidor para as redes InfiniBand  
Use estas etapas para conectar o servidor ao carregar a rede InfiniBand. Se o servidor não estiver usando a rede InfiniBand, ignore esta etapa.  
  
1.  O servidor de rack feche suficiente para o dispositivo para que você pode conectá-lo à rede InfiniBand appliance.  
  
2.  Instale o adaptador de rede InfiniBand Mellanox ConnectX-3 FDR InfiniBand para o servidor de carregamento.  
  
3.  Use os cabos FDR para conectar o adaptador de rede InfiniBand para uma das duas opções InfiniBand no primeiro rack do dispositivo.  
  
4.  Instale e configure o driver apropriado do Windows para o adaptador de rede InfiniBand.  
  
    -   InfiniBand drivers do Windows são desenvolvidos pela OpenFabrics Alliance, um consórcio do setor de fornecedores de InfiniBand.  O driver correto pode foram distribuído com o adaptador de rede InfiniBand. Caso contrário, o driver pode ser baixado do www.openfabrics.org.  
  
5.  Defina as configurações de DNS e InfiniBand para os adaptadores de rede. Para obter instruções de configuração, consulte [adaptadores de rede InfiniBand configurar](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Etapa 4: Instalar as ferramentas de carregamento  
As ferramentas de cliente estão disponíveis para download no Microsoft Download Center. 

Para instalar o dwloader, execute a instalação de dwloader das ferramentas de cliente.
  
Se você planeja usar os serviços de integração para o carregamento, você precisará instalar o Integration Services e os adaptadores de destino do Integration Services. Os adaptadores estão disponíveis nas ferramentas de cliente.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>Etapa 5: Iniciar carregamento  
Agora você está pronto para iniciar o carregamento de dados. Para obter mais informações, consulte:  
  
1.  [a ferramenta de carregamento de linha de comando de dwloader](dwloader.md)  
  
2.  [Visão geral de carga](load-overview.md)  
  
## <a name="performance"></a>Desempenho  
Para obter melhor desempenho no Windows Server 2012 e além do carregamento, ative a inicialização instantânea de arquivo para que quando os dados são substituídos, o sistema operacional não substituirá os dados existentes com zeros. Se esse é um risco de segurança porque os dados anteriores permanecem nos discos, em seguida, certifique-se desativar a inicialização instantânea de arquivo.  
  
## <a name="Security"></a>Avisos de segurança  
Como os dados ao carregar não são armazenados no dispositivo, sua equipe de TI é responsável por gerenciar todos os aspectos de segurança para seus dados ao carregar. Por exemplo, isso inclui a gerenciar a segurança dos dados para carregar, a segurança do servidor usado para armazenar carrega e a segurança da infraestrutura de rede que conecta o servidor de carregamento para o dispositivo de PDW do SQL Server.  
  
> [!IMPORTANT]  
> É especialmente importante proteger cada carregando o servidor que irá usar a ferramenta de linha de comando ao carregar dwloader. Quando dwloader carrega dados, primeiro autentica com o nó de controle e, em seguida, após a autenticação bem-sucedida que move dados do servidor de carregamento diretamente a nós de computação em canais de dados. Validação de certificado não ocorrerá durante a mão-agitação entre cada servidor de carregamento e cada nó de computação. Isso deixa os nós de computação expostos a ataques man-in-the-middle em cada canal de dados durante o carregamento. Esses ataques podem resultar em dados violados e/ou a divulgação de informações.  
  
Para reduzir os riscos de segurança com seus dados, é recomendável o seguinte:  
  
-   Designe uma conta do Windows que é usada para carregar dados em PDW. Permitir que essa conta tem permissões para o local de carga e em nenhum outro lugar.  
  
-   Designe um usuário do PDW que tenha permissões para carregar dados. Dependendo dos requisitos de segurança, você pode ter um usuário específico por banco de dados.  
  
-   Operações no servidor de carregamento podem aceitar um caminho UNC do que para extrair dados de fora da rede interna confiável. E um invasor na rede ou com capacidade para influenciar a resolução de nomes pode interceptar ou modificar os dados enviados para o SQL Server PDW. Isso apresenta um risco de divulgação de violação e informações. Violação deve ser reduzida exigindo que a conexão de assinatura. Para ajudar a reduzir esse risco, defina a seguinte opção de política de grupo **segurança Settings\Local Policies\Security Options** no servidor de carregamento: **cliente de rede Microsoft: assinar comunicações digitalmente (sempre): Habilitado**  
  
-   Desative a inicialização instantânea de arquivo no Windows Server 2012 e além. Este é um equilíbrio entre desempenho e segurança, conforme observado na seção desempenho. Você precisa decidir o que é melhor de acordo com seus requisitos de segurança.  
  
## <a name="see-also"></a>Consulte também  
[Visão geral de backup e restauração](backup-and-restore-overview.md)  
  

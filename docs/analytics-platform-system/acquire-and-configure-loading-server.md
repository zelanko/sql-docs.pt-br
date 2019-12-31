---
title: Adquirir & configurar o servidor de carregamento
description: Este artigo descreve como adquirir e configurar um servidor de carregamento como um sistema Windows que não é de dispositivo para enviar cargas de dados para o PDW (Parallel data warehouse).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef49bb86c8e16600f2ff1bf2d1c7a92ecc5af964
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401482"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>Adquirir e configurar um servidor de carregamento para data warehouse paralelos
Este artigo descreve como adquirir e configurar um servidor de carregamento como um sistema Windows que não é de dispositivo para enviar cargas de dados para o PDW (Parallel data warehouse).  
  
## <a name="Basics"></a>Algumas  
O servidor de carregamento:  
  
-   Não precisa ser um único servidor. Você pode carregar simultaneamente com vários servidores de carregamento.  
  
-   É fornecido e gerenciado por sua própria equipe de ti. Talvez você já tenha um servidor ou servidores que podem ser usados para carregar dados no PDW.  
  
-   O está localizado em seu próprio rack que não é de dispositivo e não pode ser colocado dentro do dispositivo de sistema de plataforma de análise.  
  
-   Está conectado ao dispositivo por meio da rede InfiniBand do dispositivo ou pela Ethernet. Para o desempenho, é recomendável usar o InfiniBand.  
  
-   Está em seu próprio domínio de cliente, não no domínio do dispositivo. Não há nenhuma relação de confiança entre o domínio do cliente e o domínio do dispositivo.  
  
## <a name="Step1"></a>Etapa 1: determinar os requisitos de capacidade  
O sistema de carregamento pode ser projetado como um ou mais servidores de carregamento que executam cargas simultâneas. Cada servidor de carregamento não precisa ser dedicado apenas ao carregamento, desde que ele lide com os requisitos de desempenho e armazenamento de sua carga de trabalho.  
  
Os requisitos de sistema para um servidor de carregamento dependem quase completamente da sua própria carga de trabalho. Use a [planilha de planejamento de capacidade do servidor de carregamento](loading-server-capacity-planning-worksheet.md) para ajudar a determinar seus requisitos de capacidade.  
  
## <a name="Step2"></a>Etapa 2: adquirir o Server  
Agora que você entende melhor seus requisitos de capacidade, é possível planejar os servidores e os componentes de rede que precisará comprar ou provisionar. Incorpore a lista de requisitos a seguir em seu plano de compra e, em seguida, adquira o servidor ou provisione um servidor existente.  
  
### <a name="R"></a>Requisitos de software  
Sistemas operacionais com suporte:  
  
-   Windows Server 2012 ou Windows Server 2012 R2. Esses sistemas operacionais exigem o adaptador de rede FDR.  
  
-   Windows Server 2008 R2. Este sistema operacional requer o adaptador de rede DDR.  
  
O servidor deve usar a localidade EN-US para usar a ferramenta de carregamento de linha de comando dwloader. dwloader não dá suporte a outras localidades.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Requisitos de rede para o Windows Server 2012 e o Windows Server 2012 R2  
Embora não seja necessário para carregar, InfiniBand é o tipo de conexão recomendado para o carregamento de servidores. Para obter o melhor desempenho, use o Windows Server 2012 ou o Windows Server 2012 R2 e o adaptador de rede FDR InfiniBand para conectar o servidor de carregamento à rede InfiniBand do dispositivo.  
  
Para se preparar para uma conexão do Windows Server 2012 ou do Windows Server 2012 R2 InfiniBand:  
  
1.  Planeje o servidor para o dispositivo fechar o suficiente para que você possa conectá-lo aos comutadores InfiniBand do dispositivo. Para obter mais informações sobre as tecnologias Mellanox sobre InfiniBand, consulte o White Paper, [introdução ao InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Compre um adaptador de rede de porta única ou dual de Mellanox ConnectX-3 FDR InfiniBand. É recomendável adquirir o adaptador de rede com duas portas para tolerância a falhas durante a transmissão de dados. Um adaptador de rede de duas portas é necessário para alta disponibilidade.  
  
3.  Adquira 2 cabos de InfiniBand FDR para uma placa de porta dupla ou um cabo InfiniBand de 1 FDR para um cartão de porta única. Os cabos do FDR InfiniBand conectarão o servidor de carregamento à rede InfiniBand do dispositivo. O comprimento do cabo depende da distância entre o servidor de carregamento e os comutadores InfiniBand do dispositivo, de acordo com seu ambiente.  
  
## <a name="Step3"></a>Etapa 3: conectar o servidor às redes InfiniBand  
Use estas etapas para conectar o servidor de carregamento à rede InfiniBand. Se o servidor não estiver usando a rede InfiniBand, ignore esta etapa.  
  
1.  Rack o servidor está perto o suficiente para o dispositivo para que você possa conectá-lo à rede InfiniBand do dispositivo.  
  
2.  Instale o adaptador de rede InfiniBand de InfiniBand ConnectX-3 FDR com o servidor de carregamento.  
  
3.  Use os cabos FDR para conectar o adaptador de rede InfiniBand a um dos dois comutadores InfiniBand no primeiro rack do dispositivo.  
  
4.  Instale e configure o driver do Windows apropriado para o adaptador de rede InfiniBand.  
  
    -   Os drivers InfiniBand para Windows são desenvolvidos pela OpenFabrics Alliance, um consórcio da indústria de fornecedores InfiniBand.  O driver correto pode ter sido distribuído com o adaptador de rede InfiniBand. Caso contrário, o driver pode ser baixado em www.openfabrics.org.  
  
5.  Defina as configurações de InfiniBand e DNS para os adaptadores de rede. Para obter instruções de configuração, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Etapa 4: instalar as ferramentas de carregamento  
As ferramentas de cliente estão disponíveis para download no centro de download da Microsoft. 

Para instalar o dwloader, execute a instalação do dwloader nas ferramentas de cliente.
  
Se você planeja usar Integration Services para carregar, será necessário instalar Integration Services e os adaptadores de destino Integration Services. Os adaptadores estão disponíveis nas ferramentas de cliente.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>Etapa 5: iniciar o carregamento  
Agora você está pronto para iniciar o carregamento de dados. Para obter mais informações, consulte:  
  
1.  [Ferramenta de carregamento de linha de comando dwloader](dwloader.md)  
  
2.  [Visão geral da carga](load-overview.md)  
  
## <a name="performance"></a>Desempenho  
Para um melhor desempenho de carregamento no Windows Server 2012 e posterior, ative a inicialização instantânea de arquivo para que, quando os dados forem substituídos, o sistema operacional não substitua os dados existentes por zeros. Se esse for um risco de segurança porque os dados anteriores ainda existem nos discos, certifique-se de desativar a inicialização instantânea de arquivo.  
  
## <a name="Security"></a>Avisos de segurança  
Como os dados a serem carregados não são armazenados no dispositivo, sua equipe de ti é responsável pelo gerenciamento de todos os aspectos da segurança para que seus dados sejam carregados. Por exemplo, isso inclui o gerenciamento da segurança dos dados a serem carregados, a segurança do servidor usado para armazenar cargas e a segurança da infraestrutura de rede que conecta o servidor de carregamento ao dispositivo de SQL Server PDW.  
  
> [!IMPORTANT]  
> É especialmente importante proteger cada servidor de carregamento que usará a ferramenta de carregamento de linha de comando dwloader. Quando o dwloader carrega dados, ele primeiro se autentica com o nó de controle e, após a autenticação bem-sucedida, move os dados do servidor de carregamento diretamente para os nós de computação em canais de dados. A validação de certificado não ocorre durante a disposição à mão entre cada servidor de carregamento e cada nó de computação. Isso deixa os nós de computação expostos a possíveis ataques man-in-the-Middle em cada canal de dados durante o carregamento. Esses ataques podem resultar em dados violados e/ou na divulgação de informações.  
  
Para reduzir os riscos de segurança com seus dados, aconselhamos o seguinte:  
  
-   Designe uma conta do Windows que seja usada exclusivamente com a finalidade de carregar dados no PDW. Permitir que essa conta tenha permissões para o local de carregamento e para outro lugar.  
  
-   Designe um usuário do PDW que tenha permissões para carregar dados. Dependendo dos seus requisitos de segurança, você pode ter um usuário específico por banco de dados.  
  
-   As operações no servidor de carregamento podem aceitar um caminho UNC do qual extrair dados de fora da rede interna confiável. E um invasor na rede ou com a capacidade de influenciar a resolução de nomes pode interceptar ou modificar os dados enviados para o SQL Server PDW. Isso apresenta um risco de violação e divulgação de informações. A violação deve ser mitigada exigindo a assinatura na conexão. Para ajudar a reduzir esse risco, defina a seguinte opção de política de grupo em **segurança \ Opções** de instalação no servidor de carregamento: **cliente de rede da Microsoft: assinar digitalmente as comunicações (sempre): habilitada**  
  
-   Desative a inicialização instantânea de arquivo no Windows Server 2012 e posterior. Essa é uma compensação entre desempenho e segurança, conforme observado na seção desempenho. Você precisa decidir o que é melhor de acordo com seus requisitos de segurança.  
  
## <a name="see-also"></a>Consulte Também  
[Visão geral de backup e restauração](backup-and-restore-overview.md)  
  

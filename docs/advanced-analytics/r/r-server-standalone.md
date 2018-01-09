---
title: "R Server (Autônomo) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 06/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
vms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: ca9e48f1-67b8-4905-9b78-56752d7a4e81
caps.latest.revision: "22"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: a7a7a83a1608a4505a3af0401dc8b6ac6f9c180a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="r-server-standalone"></a>R Server (Autônomo)

No SQL Server 2016, a Microsoft lançou o **R Server (autônomo)**, como parte de sua plataforma para dar suporte a análise de classe empresarial.  Microsoft R Server fornece a escalabilidade e segurança para a linguagem R e aborda as limitações de memória de software livre R. Como o SQL Server R Services, o Microsoft R Server (autônomo) fornece processamento paralelo e em partes de dados, permitindo que os usuários de R usar dados muito maiores do que pode caber na memória.

No SQL Server de 2017, foi adicionado suporte para a linguagem Python, que aproveita o amplo suporte da comunidade de máquina de aprendizado e inclui as bibliotecas populares para análises de texto e o aprendizado.  Para refletir esse conjunto mais amplo de idiomas, mudamos também o nome para **aprendizado de máquina do Microsoft Server (autônomo)**.

## <a name="benefits-of-microsoft-r-server"></a>Benefícios do Microsoft R Server

Você pode usar o Microsoft R Server para a computação distribuída em várias plataformas. Quando você instala do programa de instalação do SQL Server, você obtém o servidor baseado no Windows e todas as ferramentas necessárias para a publicação e a implantação de modelos. Para obter mais informações sobre outras plataformas, consulte estes recursos na biblioteca do MSDN:

+ [Introdução ao Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)
+ [Servidor R para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

Você também pode instalar o Microsoft R Server para usar como um cliente de desenvolvimento, para obter o RevoScaleR bibliotecas e ferramentas necessárias para criar soluções de R que podem ser implantadas para o SQL Server.

## <a name="whats-new-in-microsoft-machine-learning-server"></a>O que há de novo no Microsoft Server de aprendizado de máquina

Se você instalar os serviços de aprendizado de máquina (autônomo) usando a instalação do SQL Server 2017, você agora tem a opção de adicionar a linguagem Python. Naturalmente, a linguagem R ainda é uma opção com suporte, e você ainda pode instalar ambas as linguagens se desejado.
 
No SQL Server de 2017 CTP 2.0, a instalação do servidor também inclui o pacote de mrsdeploy e outros utilitários usados para modelos de operacionalização. Para obter mais informações, consulte [operacionalização com mrsdeploy](../../advanced-analytics/operationalization-with-mrsdeploy.md).

Usuários corporativos de aprendizado de máquina do SQL Server podem usar os instaladores para download para o Microsoft R Server para atualizar seus componentes de R, em um processo chamado associação. Para obter mais informações, consulte [SqlBindR de uso para atualização e a instância do SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

## <a name="get-microsoft-r-server-or-machine-learning-server-standalone"></a>Obter o Microsoft R Server ou servidor de aprendizado de máquina (autônomo)

 Há várias opções de instalação do Microsoft R Server:

+ Use o Assistente de instalação do SQL Server

  [Criar um R Server autônomo](../r/create-a-standalone-r-server.md)

  Execute a instalação do SQL Server 2016 para instalar **Microsoft R Server (autônomo)**. A linguagem R é adicionada por padrão.
  Ou, execute a instalação do SQL Server 2017 instalar **Server de aprendizado de máquina (autônomo)** e selecione R, Python ou ambos.

  > [!IMPORTANT]
  > A opção para instalar o servidor está no **recursos compartilhados** seção de configuração. Não instale outros componentes.
  >
  > De preferência, não instale o servidor em um computador em que SQL Server R Services ou serviços de aprendizado de máquina do SQL Server foi instalados.

+ Usar opções de linha de comando de instalação do SQL Server

  [Instalar o Microsoft R Server através da linha de comando](../r/install-microsoft-r-server-from-the-command-line.md)

  Instalação do SQL Server dá suporte a instalações autônomas por meio de um conjunto avançado de argumentos de linha de comando.

+ Use o instalador autônomo

  [Executar o Microsoft R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).

  Agora você pode usar um novo Windows installer para configurar uma nova instância do Microsoft R Server ou Microsoft Server de aprendizado de máquina.  Microsoft R Server (e Microsoft Server de aprendizado de máquina) exigem um contrato Enterprise do SQL Server. No entanto, depois de executar o instalador autônomo, a política de suporte para uma instalação existente é atualizada, para usar a nova política de ciclo de vida modernos. Essa opção de suporte garante que as atualizações para componentes de aprendizado de máquina são aplicadas com mais frequência do que ao usar as versões de serviço do SQL Server.

  
+ Atualizar uma instância do SQL Server

  [Usando SqlBindR para atualizar uma instância dos serviços do R](./use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).
  
  Você pode usar o instalador autônomo para atualizar uma instância do SQL Server 2016 R Services para usar a versão mais recente do R. Quando você executar a instalação, a política de suporte do ciclo de vida modernos será aplicada ao servidor, e os componentes de R obterá atualizações mais frequentes.
  
  > [! Observação} atualmente esse método de atualização está disponível somente para as instalações existentes do SQL Server 2016. No entanto, atualizações terão suporte para SQL Server 2017 no futuro.

## <a name="related-machine-learning-products"></a>Produtos de aprendizado de máquina relacionada

+ Máquinas virtuais do Azure com o servidor de R

  [Provisionar uma máquina Virtual do servidor R](../../advanced-analytics/r-services/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  O Azure marketplace inclui várias imagens de máquina virtual que incluem R Server. Criar uma nova máquina virtual R Server no Microsoft Azure é a maneira mais rápida de configurar um servidor para usar no desenvolvimento e implantação de modelos de previsão. Imagens vêm com recursos para o dimensionamento e compartilhamento já configurado, que torna mais fácil para inserir a análise de R dentro de aplicativos e a integração de R com sistemas de back-end.

+ Máquina de Virtual de ciência de dados

  [Máquina Virtual de ciência de dados - Windows 2016 Preview](http://aka.ms/dsvm/win2016)

  A versão mais recente da máquina Virtual de ciência de dados inclui o R Server, SQL Server, além de uma matriz das ferramentas mais populares para aprendizado de máquina, todos os pré-instalado e testado. Criar blocos de anotações do Jupyter, desenvolver soluções em Julia e usar bibliotecas de aprendizado habilitado GPU como MXNet, CNTK e TensorFlow.

## <a name="resources"></a>Recursos

Para obter mais informações sobre o Microsoft R Server, tutoriais e exemplos, consulte [produtos da Microsoft R](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started).

## <a name="see-also"></a>Consulte Também

 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)


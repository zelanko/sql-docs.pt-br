---
title: Propriedades do SQL Server (guia Avançado)
description: Saiba mais sobre as opções na guia Avançado na caixa de diálogo Propriedades do SQL Server, como o caminho de dados, a ID da instância e as propriedades personalizadas.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 2ffd10fd-bac1-478f-9cff-96ed6c8b787f
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2acca0bd84985700395cb3d073e6476167577b68
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901178"
---
# <a name="sql-server-properties-advanced-tab"></a>Propriedades do SQL Server (guia Avançado)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  As propriedades a seguir aparecem por padrão na guia **Avançado** . Se as propriedades personalizadas estiverem definidas, elas também aparecerão nessa guia com seus valores.  
  
## <a name="options"></a>Opções  
 **Clusterizado**  
 Indica se este serviço for instalado como um recurso de um servidor clusterizado.  
  
 **Relatório de Comentários do Cliente**  
 Indica se o Monitoramento da Qualidade do Serviço foi habilitado neste serviço. Para obter mais informações sobre o Relatório de Comentários do Cliente, pesquise "Configurações de relatório de erro e uso" nos Manuais Online.  
  
 **Caminho de Dados**  
 Exibe o caminho para os binários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desta instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Diretório de Despejo**  
 Exibe o local em que os despejos de memória são colocadas no caso de um erro.  
  
 **Relatório de Erros**  
 Quando definido como **Sim**, o programa Dr. Watson encaminhará informações para a [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou para o servidor de erro, se ocorrer uma falha grave. Para obter mais informações sobre o Relatório de Erros, pesquise "Configurações de relatório de erro e uso" nos Manuais Online. Para alterar esse valor, no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no seu servidor, clique em **Propriedades** e clique na página **Diversas Configurações de Servidor**. As opções são apresentadas na área **Relatório de Informações** .  
  
 **Versão do Arquivo**  
 Exibe a versão do executável do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Caminho de Instalação**  
 Exibe o caminho para os binários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desta instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **ID da Instância**  
 Indica a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usou este serviço.  
  
 **Idioma**  
 Exibe o idioma padrão das mensagens do servidor.  
  
 **Raiz do Registro**  
 Exibe o local das chaves do Registro usadas por este aplicativo.  
  
 **Nível do Service Pack**  
 Exibe o nível do service pack desta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Nome do SKU**  
 Exibe a SKU (unidade de manutenção de estoque), às vezes chamada de edição do produto.  
  
 **Parâmetros de inicialização**  
 Lista quaisquer parâmetroa usados por esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os parâmetros são separados por ponto-e-vírgulas. Entre os parâmetros padrão encontram-se os caminhos do arquivo de dados do banco de dados mestre (`master.mdf`), do arquivo de log do banco de dados mestre (`mastlog.ldf`), e do arquivo do log de erros. Para obter a sintaxe dos parâmetros de inicialização, pesquise o tópico **Usando as opções de inicialização do serviço do SQL Server**.  
  
 **Unidade de Manutenção de Estoque**  
 Exibe o número da SKU (unidade de manutenção de estoque) do produto.  
  
 **Versão**  
 Exibe o número de versão desta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Nome do Servidor Virtual**  
 **Nome do Servidor Virtual** quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado em um servidor com cluster.  
  
  

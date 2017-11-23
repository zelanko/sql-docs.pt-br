---
title: "Instalar o servidor de aprendizado de máquina (autônomo) ou Microsoft R Server (autônomo) na linha de comando | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 400f743bfbb065a5e271b5ff335d0896bb2ac3ef
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="install-machine-learning-server-standalone-or-microsoft-r-server-standalone-from-the-command-line"></a>Instalar o servidor de aprendizado de máquina (autônomo) ou Microsoft R Server (autônomo) na linha de comando

Este artigo descreve como usar argumentos de linha de comando do SQL Server para instalar os seguintes recursos do SQL Server usando a linha de comando:

+ [Server (autônomo) de aprendizado de máquina no SQL Server de 2017](#bkmk_mls2017) 
+ [Microsoft R Server (autônomo), no SQL Server 2016](#bkmk_mrs2016)

Um **autônoma** instalação exige que você especifique o local do utilitário de instalação e use os argumentos para indicar quais recursos serão instalados.

Para uma instalação **silenciosa** , forneça os mesmos argumentos e adicione o switch **/q** . Nenhum prompt é fornecido e nenhuma interação é necessária. No entanto, a instalação falhará se os argumentos necessários foram omitidos.

## <a name="prerequisites"></a>Pré-requisitos

Você deve saber como executar uma instalação de linha de comando do SQL Server e estar familiarizado com os argumentos de script.

Para obter mais informações, consulte [instalar o SQL Server a partir do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).

Se você instalar o servidor de aprendizado de máquina ou Microsoft R Server (autônomo) em um computador que tenha sem acesso à Internet, você deve baixar os componentes de R (ou Python) necessários com antecedência e copiá-los para uma pasta local. Para locais de download, consulte [instalação de componentes de aprendizado de máquina sem acesso à internet](installing-ml-components-without-internet-access.md).


## <a name="bkmk_mls2017"></a>Instalar o Microsoft Server (autônomo) de aprendizado de máquina

**Aplica-se a: SQL Server de 2017**

Execute o seguinte comando em um prompt de comando com privilégios elevados para instalar o servidor de aprendizado de máquina apenas (autônomo) e seus pré-requisitos.

+ O argumento de recursos é necessário, assim como os termos de licenciamento do SQL Server.
+ Você pode instalar um idioma, ou R e Python, mas é necessária para cada uma licença separada.

Este exemplo mostra os argumentos usados para instalar o R.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Este exemplo mostra os argumentos usados para instalar o Python.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MPY  /IACCEPTPYTHONOPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

+ Para exibir o progresso e as solicitações, remova o argumento _/q_.
+ Se você usar o argumento **recursos = SQL_SHARED_MR**, somente os componentes de servidor de aprendizado de máquina são instalados com R, nem Python. A instalação inclui todos os pré-requisitos, que são instalados silenciosamente por padrão. No entanto, é recomendável que você adicione pelo menos um idioma ao instalar pela primeira vez.
+ Adicionar **SQL_INST_MR** para instalar o suporte para R.
+ Adicionar **SQL_INST_MPY** para instalar o suporte para Python.
+ **IACCEPTROPENLICENSETERMS** indica que você aceitou os termos de licença para usar os componentes de software livre do R.
+ **IACCEPTPYTHONLICENSETERMS** indica que você aceitou os termos de licença para usar os componentes de Python.
+ **IACCEPTSQLSERVERLICENSETERMS** é necessário para executar o assistente de instalação.


## <a name="bkmk_mrs2016"></a> Instalar o Microsoft R Server (Autônomo)

**Aplica-se a: SQL Server 2016**

Execute o seguinte comando em um prompt de comando com privilégios elevados para instalar **somente** Microsoft R Server (autônomo) e seus pré-requisitos. 

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

> [!TIP]
> É recomendável que você não instalá-lo no mesmo computador que está hospedando uma instância do SQL Server R Services.

## <a name="post-installation-tasks"></a>Tarefas pós-instalação

Para configurar a outra instância do Microsoft R Server com os mesmos parâmetros, você pode usar novamente o arquivo de configuração que é criado durante a instalação. Para obter mais informações, consulte [instalar o SQL Server usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md).

### <a name="review-installed-components"></a>Componentes de análise instalado

Após a conclusão da instalação, você pode examinar o arquivo de configuração criado pela instalação do SQL Server, juntamente com um resumo das ações de instalação.

Por padrão, todos os resumos e logs de instalação do SQL Server e os recursos relacionados são criados nas seguintes pastas:

+ 2017 do SQL Server:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`
+ SQL Server 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`

Uma subpasta separada é criada para cada recurso que você instalou.

### <a name="customize-the-r-or-python-environment"></a>Personalizar o ambiente de R ou Python

Após a instalação, você pode instalar outros pacotes de R ou Python. O processo difere um pouco dependendo se você estiver usando o SQL Server 2016 ou 2017 do SQL Server.

No SQl Server de 2017, você pode instalar e gerenciar pacotes de R usando o T-SQL. Para obter mais informações, consulte [instalando e Gerenciando pacotes R](../r/install-additional-r-packages-on-sql-server.md).

Para Python e no SQL Server 2016, um administrador deve instalar qualquer bibliotecas adicionais que podem ser necessárias.

> [!IMPORTANT]
> Se você pretende executar seu código R no SQL Server, certifique-se de que você instale os mesmos pacotes no computador que você usará para desenvolver a solução e a instância do SQL Server em que você executar ou implantar a solução.

### <a name="upgrading-r-server-or-sql-server-machine-learning"></a>Atualizando o aprendizado de máquina do servidor de R ou do SQL Server

Se você não pretende usar o SQL Server, você pode instalar o Microsoft R Server ou o servidor de aprendizado de máquina usando um instalador separado do Windows. Para locais de download e instruções, consulte estes links:

+ [Instalar o servidor para Windows de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar o servidor de R 9.0.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) 

O instalador do windows separado para o servidor de aprendizado de máquina também pode ser usado para atualizar a componentes associados com a instância de aprendizado de máquina.  Para obter mais informações, consulte estes links:

+ [Use SqlBindR para atualizar o R](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

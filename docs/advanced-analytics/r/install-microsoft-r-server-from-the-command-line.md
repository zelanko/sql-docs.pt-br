---
title: "Instalar o Microsoft R Server através da linha de comando | Microsoft Docs"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: b9f6ceba4d3609a7e7ff816d31446a77c4fea64c
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="install-microsoft-r-server-from-the-command-line"></a>Instalar o Microsoft R Server na Linha de comando
    
Este tópico descreve como usar argumentos de linha de comando do SQL Server para instalar o Microsoft R Server no SQL Server 2016 ou instalar o servidor de aprendizado de máquina (autônomo) no SQL Server 2017. 

> [!NOTE]
Você também pode instalar o Microsoft R Server usando um instalador separado do Windows. Para obter mais informações, consulte [instalar servidor R 9.0.1 para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows). 

## <a name="prerequisites"></a>Pré-requisitos

Esse método de instalação requer que você sabe como executar uma instalação de linha de comando do SQL Server e estiver familiarizado com os argumentos de script.

- A instalação**Autônoma** exige que você especifique o local do utilitário de instalação e use argumentos para indicar quais recursos serão instalados. 
- Para uma instalação **silenciosa** , forneça os mesmos argumentos e adicione o switch **/q** . Nenhum aviso será fornecido e não é necessária nenhuma interação. No entanto, a instalação falhará se os argumentos necessários forem omitidos.

Para obter mais informações, consulte [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## <a name="sql-server-2017-microsoft-machine-learning-server-standalone"></a>SQL Server 2017: Máquina do Microsoft aprendizado Server (autônomo)

Execute o seguinte comando em um prompt de comando com privilégios elevados para instalar apenas Microsoft Machine Learning Server (autônomo) e seus pré-requisitos.  O exemplo mostra os argumentos usados para instalar o R.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```

Para exibir o progresso e as solicitações, remova o argumento _/q_.

- **RECURSOS = SQL_SHARED_MR** obtém somente os componentes de servidor de aprendizado de máquina. Isso inclui todos os pré-requisitos que são instalados silenciosamente por padrão.
- **SQL_INST_MR** é necessária para suportar installl da linguagem R.
- **SQL_INST_MPY** é necessário para instalar o suporte para Python.
- **IACCEPTROPENLICENSETERMS** indica que você aceitou os termos de licença para usar os componentes de software livre do R.
- **IACCEPTPYTHONLICENSETERMS** indica que você aceitou os termos de licença para usar os componentes de Python.
- **IACCEPTSQLSERVERLICENSETERMS** é necessário para executar o assistente de instalação.

**Observações**

1. O argumento de recursos é necessário, assim como os termos de licenciamento do SQL Server.
2. Especifique pelo menos um idioma, junto com o sinalizador de contrato de licenciamento.
3. Você pode instalar um idioma, ou R e Python, mas é necessária para cada uma licença separada.

## <a name="sql-server-2016-microsoft-r-server-standalone"></a>SQL Server 2016: Microsoft R Server (autônomo)

Execute o seguinte comando, em um prompt de comandos com privilégios elevados, para instalar somente o Microsoft R Server (Autônomo) e seus pré-requisitos.  O exemplo mostra os argumentos usados com a instalação do SQL Server 2016.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

## <a name="offline-installation"></a>Instalação offline

Se você instalar o servidor de aprendizado de máquina ou Microsoft R Server (autônomo) em um computador que tenha sem acesso à Internet, você deve baixar os componentes de R necessários com antecedência e copiá-los para uma pasta local. Para locais de download, consulte [Instalando componentes do R sem acesso à Internet](../r/installing-ml-components-without-internet-access.md).

## <a name="what-is-installed"></a>O que é instalado

Após a conclusão da instalação, você pode examinar o arquivo de configuração criado pela instalação do SQL Server, juntamente com um resumo das ações de instalação.

Por padrão, todos os resumos e logs de instalação do SQL Server e os recursos relacionados são criados nas seguintes pastas:

- SQL Server 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`
- 2017 do SQL Server:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`

Uma subpasta separada é criada para cada recurso instalado.

Para configurar a outra instância do Microsoft R Server com os mesmos parâmetros, você pode usar novamente o arquivo de configuração que é criado durante a instalação. Para obter mais informações, consulte [instalar o SQL Server usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)


## <a name="customize-your-r-environment"></a>Personalizar o seu ambiente de R

Após a instalação, você pode instalar pacotes do R adicionais. Para obter mais informações, consulte [Instalando e Gerenciando pacotes de R](../r/install-additional-r-packages-on-sql-server.md).

> [!IMPORTANT]
> Se você pretende executar seu código R no SQL Server, certifique-se de que você instale os mesmos pacotes no computador que você usará para desenvolver a solução e a instância do SQL Server em que você executar ou implantar a solução.

Depois de ter instalado os serviços de aprendizado de máquina para R (no banco de dados), você pode usar o Windows installer separado para atualizar a versão do R que está associado uma instância especificada do SQL Server. Para obter mais informações, consulte [SqlBindR de uso para atualizar R](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).




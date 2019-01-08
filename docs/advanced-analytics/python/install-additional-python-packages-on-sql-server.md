---
title: Instalar novos pacotes de linguagem Python - aprendizagem de máquina do SQL Server
description: Adicione novos pacotes de Python para SQL Server 2017 Machine Learning Services (no banco de dados) e Machine Learning Server (autônomo).
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fc038f94fc24b8c0f795efc18c62acc1656877a7
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432309"
---
# <a name="install-new-python-packages-on-sql-server"></a>Instalar novos pacotes de Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como instalar novos pacotes de Python em uma instância do SQL Server 2017 Machine Learning Services. Em geral, o processo de instalação de novos pacotes é semelhante àquela em um ambiente padrão do Python. No entanto, algumas etapas adicionais serão necessárias se o servidor não tiver uma conexão de internet.

Para obter mais informações sobre os caminhos de local e a instalação do pacote, consulte [obter R ou Python informações do pacote](../r/determine-which-packages-are-installed-on-sql-server.md).

## <a name="prerequisites"></a>Prerequisites

+ [Serviços SQL Server 2017 Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md) com a opção de linguagem Python. 

+ Pacotes devem estar em conformidade com a 3.5 e execute o Python no Windows. 

+ Acesso administrativo ao servidor é necessário para instalar pacotes.

## <a name="considerations"></a>Considerações

Antes de adicionar pacotes, considere se o pacote é uma boa opção para o ambiente do SQL Server. Normalmente, um servidor de banco de dados é um recurso compartilhado acomodar cargas de trabalho. Se você adicionar pacotes que colocam pressão excessiva computacional no servidor, o desempenho sofrerá. 

Além disso, alguns pacotes de Python populares (como Flask) realizar tarefas, como o desenvolvimento da web, que são mais adequadas para um ambiente autônomo. É recomendável que você use o Python no banco de dados para tarefas que se beneficiam de uma forte integração com o mecanismo de banco de dados, como o aprendizado de máquina, em vez de tarefas que simplesmente consultar o banco de dados.

Servidores de banco de dados são bloqueados com frequência. Em muitos casos, o acesso à Internet é bloqueado inteiramente. Para pacotes com uma longa lista de dependências, você precisará identificar essas dependências com antecedência e estar disposto a instalar cada um deles manualmente.

## <a name="add-a-new-python-package"></a>Adicionar um novo pacote do Python

Neste exemplo, vamos supor que você deseja instalar um novo pacote diretamente no computador do SQL Server.

Instalação do pacote é por instância. Se você tiver várias instâncias de serviços de Machine Learning, você deve adicionar o pacote para cada um deles.

O pacote instalado neste exemplo é [CNTK](https://docs.microsoft.com/cognitive-toolkit/), uma estrutura para aprendizado aprofundado da Microsoft que oferece suporte à personalização, treinamento e o compartilhamento de tipos diferentes de redes neurais.

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>Etapa 1. Baixe a versão do Windows do pacote do Python

+ Se você estiver instalando os pacotes do Python em um servidor sem acesso à internet, você deve baixar o arquivo WHL para um computador diferente e, em seguida, copie-o para o servidor.

    Por exemplo, em um computador separado, você pode baixar o arquivo WHL deste site [ https://cntk.ai/PythonWheel/CPU-Only ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)e, em seguida, copie o arquivo `cntk-2.1-cp35-cp35m-win_amd64.whl` para uma pasta local no computador do SQL Server.

+ SQL Server 2017 usa Python 3.5. 

> [!IMPORTANT]
> Certifique-se de que você obtenha a versão do Windows do pacote. Se o arquivo terminar em gz, provavelmente não é a versão correta.

Esta página contém os downloads para várias plataformas e para várias versões do Python: [Configurar o CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>Etapa 2. Abra um prompt de comando do Python

Localize o local da biblioteca Python padrão usado pelo SQL Server. Se você tiver instalado várias instâncias, localize a pasta PYTHON_SERVICE para a instância onde você deseja adicionar o pacote.

Por exemplo, se os serviços de Machine Learning foi instalado usando os padrões e aprendizado de máquina é habilitado na instância padrão, o caminho seria da seguinte maneira:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Abra o prompt de comando do Python associado à instância.

> [!TIP]
> Para futuras depuração e teste, você talvez queira configurar um ambiente do Python específico para a biblioteca de instância.

### <a name="step-3-install-the-package-using-pip"></a>Etapa 3. Instale o pacote usando o pip

+ Se você estiver acostumado a usar a linha de comando do Python, use PIP.exe para instalar novos pacotes. Você pode encontrar o **pip** instalador a `Scripts` subpasta. 

  Instalação do SQL Server não adicionar Scripts ao caminho do sistema. Se você receber um erro que `pip` não é reconhecido como um comando interno ou externo, você pode adicionar a pasta de Scripts para a variável de caminho no Windows.

  O caminho completo do **Scripts** pasta em uma instalação padrão é o seguinte:

    Server\MSSQL14 SQL do C:\Program Files\Microsoft. MSSQLSERVER\PYTHON_SERVICES\Scripts

+ Se você estiver usando o Visual Studio 2017 ou Visual Studio 2015 com as extensões do Python, você pode executar `pip install` do **ambientes do Python** janela. Clique em **pacotes**e na caixa de texto, forneça o nome ou local do pacote a instalar. Você não precisa digitar `pip install`; ele é preenchido para você automaticamente. 

    - Se o computador tiver acesso à Internet, forneça o nome do pacote, ou a URL de um pacote específico e uma versão. 
    
    Por exemplo, para instalar a versão do CNTK com suporte para Windows e o Python 3.5, especifique a URL de download: `https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - Se o computador não tiver acesso à internet, você deve baixar o arquivo WHL antes de iniciar a instalação. Em seguida, especifique o nome e caminho do arquivo local. Por exemplo, cole o seguinte caminho e arquivo para instalar o arquivo WHL baixado do site: `"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

Você pode ser solicitado a elevar as permissões para concluir a instalação.

À medida que progride de instalação, você pode ver mensagens de status na janela do prompt de comando:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>Etapa 4. Carregar o pacote ou suas funções como parte do script

Quando a instalação for concluída, você pode começar imediatamente usando o pacote conforme descrito na próxima etapa.

Para obter exemplos de aprendizagem profunda usando CNTK, consulte estes tutoriais: [API do Python para o CNTK](https://cntk.ai/pythondocs/tutorials.html)

Para usar funções do pacote em seu script, insira o padrão `import <package_name>` instrução nas linhas iniciais do script:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>Listar os pacotes instalados usando conda

Há diferentes maneiras que você pode obter uma lista de pacotes instalados. Por exemplo, você pode exibir os pacotes instalados na **ambientes do Python** windows do Visual Studio.

Se você estiver usando a linha de comando do Python, você pode usar **Pip** ou o **conda** Gerenciador de pacotes, incluído com o ambiente do Anaconda Python adicionado pela instalação do SQL Server.

1. Vá para C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. Clique com botão direito **conda.exe** > **executar como administrador**e insira `conda list` para retornar uma lista de pacotes instalados no ambiente atual.

1. Da mesma forma, clique com botão direito **pip.exe** > **executar como administrador**e insira `pip list` para retornar as mesmas informações. 

Para obter mais informações sobre **conda** e como usá-lo para criar e gerenciar vários ambientes do Python, consulte [gerenciamento de ambientes de conda](https://conda.io/docs/user-guide/tasks/manage-environments.html).

> [!Note]
> Instalação do SQL Server não adiciona o Pip ou Conda ao caminho do sistema e em uma instância do SQL Server de produção, manter os executáveis não essenciais fora do caminho é uma prática recomendada. No entanto, para ambientes de desenvolvimento e teste, você pode adicionar a pasta de Scripts para a variável de ambiente do caminho de sistema para executar o Pip e Conda no comando de qualquer local.

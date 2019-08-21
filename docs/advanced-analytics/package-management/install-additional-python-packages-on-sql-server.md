---
title: Instalar novos pacotes de idioma do Python
description: Adicione novos pacotes do Python ao SQL Server Serviços de Machine Learning (no banco de dados) e Machine Learning Server (autônomo).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e107622655d5f00d27de6abcea46a92526f47ada
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641193"
---
# <a name="install-new-python-packages-on-sql-server"></a>Instalar novos pacotes do Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como instalar novos pacotes do Python em uma instância do SQL Server Serviços de Machine Learning. Em geral, o processo de instalação de novos pacotes é semelhante ao de um ambiente padrão do Python. No entanto, algumas etapas adicionais serão necessárias se o servidor não tiver uma conexão com a Internet.

Para obter mais informações sobre o local do pacote e caminhos de instalação, consulte [obter informações do pacote R ou Python](../package-management/installed-package-information.md).

## <a name="prerequisites"></a>Pré-requisitos

+ [SQL Server serviços de Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md) com a opção de linguagem Python. 

+ Os pacotes devem ser compatíveis com Python 3,5 e ser executados no Windows. 

+ O acesso administrativo ao servidor é necessário para instalar pacotes.

## <a name="considerations"></a>Considerações

Antes de adicionar pacotes, considere se o pacote é uma boa opção para o ambiente de SQL Server. Normalmente, um servidor de banco de dados é um ativo compartilhado que acomoda várias cargas de trabalho. Se você adicionar pacotes que colocam muita pressão computacional no servidor, o desempenho será prejudicado. 

Além disso, alguns pacotes do Python populares (como Flask) executam tarefas, como o desenvolvimento para a Web, que são mais adequados para um ambiente autônomo. Recomendamos que você use o Python no banco de dados para tarefas que se beneficiam da forte integração com o mecanismo de banco de dados, como o Machine Learning, em vez de tarefas que simplesmente consultam o banco de dados.

Os servidores de banco de dados são freqüentemente bloqueados. Em muitos casos, o acesso à Internet é totalmente bloqueado. Para pacotes com uma longa lista de dependências, você precisará identificar essas dependências antecipadamente e estar disposto a instalar cada uma manualmente.

## <a name="add-a-new-python-package"></a>Adicionar um novo pacote do Python

Para este exemplo, presumimos que você deseja instalar um novo pacote diretamente no computador SQL Server.

A instalação do pacote é por instância. Se você tiver várias instâncias do Serviços de Machine Learning, deverá adicionar o pacote a cada uma delas.

O pacote instalado neste exemplo é [CNTK](https://docs.microsoft.com/cognitive-toolkit/), uma estrutura para aprendizado profundo da Microsoft que dá suporte à personalização, ao treinamento e ao compartilhamento de diferentes tipos de redes neurais.

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>Etapa 1. Baixar a versão do Windows do pacote do Python

+ Se você estiver instalando pacotes do Python em um servidor sem acesso à Internet, você deve baixar o arquivo WHL em um computador diferente e, em seguida, copiá-lo para o servidor.

    Por exemplo, em um computador separado, você pode baixar o arquivo WHL desse site [https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)e, em seguida, copiar o arquivo `cntk-2.1-cp35-cp35m-win_amd64.whl` para uma pasta local no computador SQL Server.

+ SQL Server 2017 usa o Python 3,5. 

> [!IMPORTANT]
> Certifique-se de obter a versão do Windows do pacote. Se o arquivo terminar em. gz, provavelmente não é a versão correta.

Esta página contém downloads para várias plataformas e várias versões do Python: [Configurar o CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>Etapa 2. Abrir um prompt de comando do Python

Localize o local da Biblioteca Python padrão usado pelo SQL Server. Se você tiver instalado várias instâncias, localize a pasta PYTHON_SERVICE para a instância em que você deseja adicionar o pacote.

Por exemplo, se Serviços de Machine Learning tiver sido instalado usando padrões e o Machine Learning estiver habilitado na instância padrão, o caminho será o seguinte:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Abra o prompt de comando do Python associado à instância.

> [!TIP]
> Para depuração e teste futuros, talvez você queira configurar um ambiente do Python específico para a biblioteca de instâncias.

### <a name="step-3-install-the-package-using-pip"></a>Etapa 3. Instalar o pacote usando Pip

+ Se você estiver acostumado a usar a linha de comando do Python, use PIP. exe para instalar novos pacotes. Você pode encontrar o instalador de **Pip** na `Scripts` subpasta. 

  SQL Server configuração não adiciona scripts ao caminho do sistema. Se você receber um erro que `pip` não seja reconhecido como um comando interno ou externo, poderá adicionar a pasta scripts à variável path no Windows.

  O caminho completo da pasta **scripts** em uma instalação padrão é o seguinte:

    C:\Arquivos de Programas\microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

+ Se você estiver usando o Visual Studio 2017 ou o Visual Studio 2015 com as extensões do Python, poderá `pip install` executar a partir da janela **ambientes do python** . Clique em **pacotes**e, na caixa de texto, forneça o nome ou o local do pacote a ser instalado. Você não precisa digitar `pip install`; ele é preenchido para você automaticamente. 

    - Se o computador tiver acesso à Internet, forneça o nome do pacote ou a URL de um pacote e versão específicos. 
    
    Por exemplo, para instalar a versão do CNTK que tem suporte para Windows e Python 3,5, especifique a URL de download:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - Se o computador não tiver acesso à Internet, você deverá baixar o arquivo WHL antes de iniciar a instalação. Em seguida, especifique o caminho e o nome do arquivo local. Por exemplo, Cole o seguinte caminho e arquivo para instalar o arquivo WHL baixado do site:`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

Você pode ser solicitado a elevar as permissões para concluir a instalação.

À medida que a instalação progride, você pode ver as mensagens de status na janela do prompt de comando:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>Etapa 4. Carregar o pacote ou suas funções como parte do seu script

Quando a instalação for concluída, você poderá começar imediatamente a usar o pacote, conforme descrito na próxima etapa.

Para obter exemplos de aprendizado profundo usando o CNTK, consulte estes tutoriais: [API do Python para CNTK](https://cntk.ai/pythondocs/tutorials.html)

Para usar funções do pacote em seu script, insira a instrução padrão `import <package_name>` nas linhas iniciais do script:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>Listar pacotes instalados usando o Conda

Há diferentes maneiras pelas quais você pode obter uma lista de pacotes instalados. Por exemplo, você pode exibir os pacotes instalados nas janelas de **ambientes do Python** do Visual Studio.

Se você estiver usando a linha de comando do Python, poderá usar o **Pip** ou o Gerenciador de pacotes **Conda** , incluído no ambiente Anaconda Python adicionado pela instalação do SQL Server.

1. Vá para C:\Arquivos de Programas\microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. Clique com o botão direito do mouse em **Conda. exe** > **Executar como administrador**e digite `conda list` para retornar uma lista de pacotes instalados no ambiente atual.

1. Da mesma forma, clique com o botão direito do mouse em **Pip. exe** > **Executar como administrador**e digite `pip list` para retornar as mesmas informações. 

Para obter mais informações sobre **Conda** e como você pode usá-lo para criar e gerenciar vários ambientes de Python, consulte [Gerenciando ambientes com o Conda](https://conda.io/docs/user-guide/tasks/manage-environments.html).

> [!Note]
> SQL Server configuração não adiciona PIP ou Conda ao caminho do sistema e em uma instância de SQL Server de produção, manter os executáveis não essenciais fora do caminho é uma prática recomendada. No entanto, para ambientes de desenvolvimento e teste, você pode adicionar a pasta scripts à variável de ambiente PATH do sistema para executar o Pip e o Conda no comando de qualquer local.

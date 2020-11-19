---
title: Instalar pacotes com ferramentas do Python
description: Saiba como usar as ferramentas padrão do Python para instalar novos pacotes do Python em uma instância dos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/21/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 67d5a323cfdbdb7eb765430ba264ff0bde2074f5
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870474"
---
# <a name="install-packages-with-python-tools-on-sql-server"></a>Instalar pacotes com ferramentas do Python no SQL Server
[!INCLUDE [SQL Server 2017 only](../../includes/applies-to-version/sqlserver2017-only.md)]

Este artigo descreve como usar as ferramentas padrão do Python para instalar novos pacotes do Python em uma instância dos Serviços de Machine Learning do SQL Server. No geral, o processo de instalação de novos pacotes é semelhante ao de um ambiente padrão do Python. No entanto, algumas etapas adicionais serão necessárias se o servidor não tiver uma conexão com a Internet.

Para obter mais informações sobre a localização e os caminhos de instalação do pacote, confira [Obter informações do pacote de Python](python-package-information.md).

## <a name="prerequisites"></a>Prerequisites

+ Você precisa ter os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) instalados com a opção de linguagem do Python.

### <a name="other-considerations"></a>Outras considerações

+ Os pacotes precisam ter conformidade com Python 3.5 e ser executados no Windows.

+ A biblioteca de pacotes de Python está localizada na pasta Arquivos de Programas de sua instância do SQL Server e, por padrão, a instalação nessa pasta requer permissões de administrador. Para obter mais informações, confira [Localização da biblioteca de pacotes](../package-management/python-package-information.md#default-python-library-location).

+ A instalação do pacote é feita por instância. Se tiver várias instâncias do Serviços de Machine Learning, você deverá adicionar o pacote a cada uma delas.

+ Os servidores de banco de dados frequentemente são bloqueados. Em muitos casos, o acesso à Internet é totalmente bloqueado. Para pacotes com uma longa lista de dependências, você precisará identificar essas dependências antecipadamente e estar preparado para instalar cada uma manualmente.

+ Antes de adicionar um pacote, considere se ele é uma boa opção para o ambiente do SQL Server.

  + Recomendamos que você use o Python no banco de dados para tarefas que se beneficiam da forte integração com o mecanismo de banco de dados, como o aprendizado de máquina, em vez de tarefas que simplesmente consultam o banco de dados.

  + Se você adicionar pacotes que colocam muita pressão computacional sobre o servidor, o desempenho será prejudicado.

  + Em um ambiente do SQL Server protegido, talvez você queira evitar o seguinte:
    + Pacotes que exigem acesso à rede
    + Pacotes que exigem acesso elevado ao sistema de arquivos
    + Pacotes usados para desenvolvimento Web ou outras tarefas que não se beneficiam da execução dentro do SQL Server

## <a name="add-a-python-package-on-sql-server"></a>Adicionar um pacote de Python ao SQL Server

Para instalar um novo pacote do Python que pode ser usado em um script no SQL Server, instale o pacote na instância dos Serviços de Machine Learning. Se tiver várias instâncias do Serviços de Machine Learning, você deverá adicionar o pacote a cada uma delas.

O pacote instalado nos exemplos a seguir é o [CNTK](/cognitive-toolkit/), uma estrutura para aprendizado profundo da Microsoft compatível com a personalização, com o treinamento e com o compartilhamento de diferentes tipos de redes neurais.

### <a name="for-offline-install-download-the-python-package"></a>Para a instalação offline, baixe o pacote do Python

Se você estiver instalando pacotes do Python em um servidor sem acesso à Internet, precisará baixar o arquivo WHL de um computador com acesso à Internet e copiá-lo para o servidor.

Por exemplo, em um computador conectado à Internet, você pode baixar o arquivo `cntk-2.1-cp35-cp35m-win_amd64.whl` do site [https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl) e, em seguida, copiar o arquivo para uma pasta local no computador do SQL Server.

> [!IMPORTANT]
> Certifique-se de obter a versão do Windows do pacote. Se o arquivo terminar em .gz, provavelmente não é a versão correta.

Para obter mais informações sobre downloads da estrutura do CNTK para várias plataformas e várias versões do Python, confira [Configurar o CNTK em seu computador](/cognitive-toolkit/Setup-CNTK-on-your-machine).

### <a name="locate-the-python-library"></a>Localizar a biblioteca do Python

Encontre a localização padrão da Biblioteca Python usada pelo SQL Server. Se você tiver instalado várias instâncias, localize a pasta `PYTHON_SERVICES` para a instância em que você deseja adicionar o pacote.

Por exemplo, se os Serviços de Machine Learning foram instalados usando padrões e o Machine Learning foi habilitado na instância padrão, o caminho é:

```console
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"
```

> [!TIP]
> Para depuração e teste futuros, talvez você queira configurar um ambiente do Python específico para a biblioteca de instâncias.

### <a name="install-the-package-using-pip"></a>Instalar o pacote usando pip

Use o instalador **pip** para instalar novos pacotes. Você pode encontrar `pip.exe` na subpasta `Scripts` da pasta `PYTHON_SERVICES`. A instalação do SQL Server não adiciona a subpasta `Scripts` ao caminho do sistema, portanto, é necessário especificar o caminho completo ou você pode adicionar a pasta Scripts à variável PATH no Windows.

> [!NOTE]
> Se você estiver usando o Visual Studio 2017 ou o Visual Studio 2015 com as extensões do Python, poderá executar `pip install` na janela de **Ambientes do Python**. Clique em **Pacotes** e, na caixa de texto, forneça o nome ou a localização do pacote a ser instalado. Você não precisa digitar `pip install`. Ele é preenchido para você automaticamente.

+ Se o computador tiver acesso à Internet, forneça o nome do pacote:

  ```console
  scripts\pip.exe install cntk
  ```
  Você também pode especificar a URL de um pacote e versão específicos, por exemplo:

  ```console
  scripts\pip.exe install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  ```

+ Se o computador não tiver acesso à Internet, especifique o arquivo WHL que você baixou anteriormente. Por exemplo:

  ```console
  scripts\pip.exe install C:\Downloads\cntk-2.1-cp35-cp35m-win_amd64.whl
  ```

Pode ser solicitado que você eleve as permissões para concluir a instalação.
Conforme a instalação progride, você pode ver as mensagens de status na janela do prompt de comando.

### <a name="load-the-package-or-its-functions-as-part-of-your-script"></a>Carregar o pacote ou suas funções como parte do seu script

Quando a instalação for concluída, você poderá começar imediatamente a usar o pacote em scripts do Python no SQL Server.

Para usar funções do pacote em seu script, insira a instrução de `import <package_name>` padrão nas linhas iniciais do script:

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import cntk
# Python statements ...
'
```

## <a name="see-also"></a>Confira também

+ [Obter informações sobre o pacote do Python](python-package-information.md)
+ [Tutoriais de Python para os Serviços de Machine Learning do SQL Server](../tutorials/python-tutorials.md)
+ [API do Python para CNTK](https://cntk.ai/pythondocs/tutorials.html).
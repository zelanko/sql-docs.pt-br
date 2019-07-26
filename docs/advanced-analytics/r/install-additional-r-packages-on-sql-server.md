---
title: Instalar novos pacotes de linguagem R
description: Adicionar novos pacotes de R a SQL Server 2016 R Services ou SQL Server 2017 Serviços de Machine Learning (no banco de dados)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1a6459d45d36ff69bdafb62a712e18937bf8eb30
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470108"
---
# <a name="install-new-r-packages-on-sql-server"></a>Instalar novos pacotes R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como instalar novos pacotes do R em uma instância do SQL Server em que o Machine Learning está habilitado. Há vários métodos para instalar novos pacotes de R, dependendo de qual versão do SQL Server você tem e se o servidor tem uma conexão com a Internet. As abordagens a seguir para a instalação de novo pacote são possíveis.

| Abordagem                           | Permissões               | Remoto/local |
|------------------------------------|---------------------------|--------------|
| [Usar gerenciadores de pacotes R convencionais](use-r-package-managers-on-sql-server.md)  | Admin | Local |
| [Usar RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Habilitado para administrador, funções de banco de dados posteriormente | both|
| [Usar o T-SQL (criar biblioteca externa)](install-r-packages-tsql.md) | Habilitado para administrador, funções de banco de dados posteriormente | both 

## <a name="who-installs-permissions"></a>Quem instala o (permissões)

A biblioteca de pacotes do R está localizada fisicamente na pasta arquivos de programas da sua SQL Server instância, em uma pasta segura com acesso restrito. A gravação nesse local requer permissões de administrador.

Não administradores podem instalar pacotes, mas isso requer configuração adicional e funcionalidade não disponível em instalações iniciais. Há duas abordagens para instalações de pacotes não-administradores: RevoScaleR usando a versão 9.0.1 e posterior ou usando criar biblioteca externa (somente SQL Server 2017). No SQL Server 2017, **dbo_owner** ou outro usuário com a permissão Criar biblioteca externa pode instalar pacotes R no banco de dados atual.

Os desenvolvedores de R estão acostumados a criar bibliotecas de usuários para os pacotes de que precisam se as bibliotecas localizadas de forma centralizada estiverem fora dos limites. Essa prática é problemática para o código R em execução em uma instância do mecanismo de banco de dados SQL Server. SQL Server não pode carregar pacotes de bibliotecas externas, mesmo se essa biblioteca estiver no mesmo computador. Somente os pacotes da biblioteca de instâncias podem ser usados em código R em execução no SQL Server.

O acesso ao sistema de arquivos normalmente é restrito no servidor e, mesmo que você tenha direitos de administrador e acesso a uma pasta de documentos do usuário no servidor, o tempo de execução de script externo que é executado no SQL Server não pode acessar nenhum pacote instalado fora da instância padrão biblioteca. 

## <a name="considerations-for-package-installation"></a>Considerações sobre a instalação do pacote

Antes de instalar novos pacotes, considere se os recursos habilitados por um determinado pacote são adequados em um ambiente de SQL Server. Em um ambiente de SQL Server protegido, talvez você queira evitar o seguinte:

+ Pacotes que exigem acesso à rede
+ Pacotes que exigem acesso elevado ao sistema de arquivos
+ O pacote é usado para desenvolvimento na Web ou outras tarefas que não se beneficiam com a execução dentro de SQL Server

## <a name="offline-installation-no-internet-access"></a>Instalação offline (sem acesso à Internet)

Em geral, os servidores que hospedam bancos de dados de produção bloqueiam as conexões de Internet. A instalação de novos pacotes R ou Python em tais ambientes requer que você prepare pacotes e dependências com antecedência e copie os arquivos para uma pasta no servidor para instalação offline.

A identificação de todas as dependências é complicada. Para o R, recomendamos que você use [o miniCRAN para criar um repositório local](create-a-local-package-repository-using-minicran.md) e, em seguida, transfira o repositório totalmente definido para uma instância de SQL Server isolada.

Como alternativa, você pode executar estas etapas manualmente:

1. Identifique todas as dependências de pacote. 
2. Verifique se os pacotes necessários já estão instalados no servidor. Se o pacote estiver instalado, verifique se a versão está correta.
3. Baixe o pacote e todas as dependências em um computador separado.
4. Mova os arquivos para uma pasta acessível pelo servidor.
5. Execute um comando de instalação com suporte ou uma instrução DDL para instalar o pacote na biblioteca de instâncias.

### <a name="download-the-package-as-a-zipped-file"></a>Baixar o pacote como um arquivo compactado

Para a instalação em um servidor sem acesso à Internet, você deve baixar uma cópia do pacote no formato de um arquivo compactado para instalação offline. **Não Descompacte o pacote.**

Por exemplo, o procedimento a seguir descreve agora para obter a versão correta do pacote [FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) do biocondutor, supondo que o computador tenha acesso à Internet.

1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .

2.  Clique com o botão direito do mouse no link para o. Arquivo ZIP e selecione **Salvar destino como**.

3.  Navegue até a pasta local onde os pacotes compactados são armazenados e clique em **salvar**.

    Esse processo cria uma cópia local do pacote. 

4. Se você receber um erro de download, tente um site de espelhamento diferente.

5. Depois que o arquivo de pacote for baixado, você poderá instalar o pacote ou copiar o pacote compactado para um servidor que não tenha acesso à Internet.

> [!TIP]
> Se, por engano, você instalar o pacote em vez de baixar os binários, uma cópia do arquivo compactado baixado também será salva em seu computador. Observe as mensagens de status conforme o pacote é instalado para determinar o local do arquivo. Você pode copiar esse arquivo compactado para o servidor que não tem acesso à Internet.
> 
> No entanto, quando você obtém pacotes usando esse método, as dependências não são incluídas. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Instalação lado a lado com servidores R ou Python autônomos

Os recursos de R e Python estão incluídos em vários produtos da Microsoft, que podem coexistir no mesmo computador.

Se você instalou SQL Server 2017 Microsoft Machine Learning Server (autônomo) ou SQL Server servidor R 2016 (autônomo), além da análise no banco de dados (SQL Server 2017 Serviços de Machine Learning e SQL Server 2016 R Services), seu computador terá instalações de R para cada, com duplicatas de todas as ferramentas e bibliotecas de R.

Os pacotes instalados na biblioteca R_SERVER são usados somente por um servidor autônomo e não podem ser acessados por uma instância SQL Server (no banco de dados). Sempre use a `R_SERVICES` biblioteca ao instalar pacotes que você deseja usar no banco de dados no SQL Server. Para obter mais informações sobre caminhos, consulte [local da biblioteca de pacotes](../package-management/default-packages.md).

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)

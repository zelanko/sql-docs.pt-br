---
title: Instalar novos pacotes de idioma R - serviços do SQL Server Machine Learning
description: Adicionar novos pacotes de R para SQL Server 2016 R Services ou serviços SQL Server 2017 Machine Learning (no banco de dados)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 218003efa75ead5ab795fa5ef10ac09c4d97a6a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962623"
---
# <a name="install-new-r-packages-on-sql-server"></a>Instalar novos pacotes de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como instalar novos pacotes de R em uma instância do SQL Server em que o aprendizado de máquina está habilitado. Há vários métodos para instalar novos pacotes de R, dependendo de qual versão do SQL Server que você tem e se o servidor tem uma conexão de internet. As seguintes abordagens para a nova instalação do pacote são possíveis.

| Abordagem                           | Permissões               | Remoto/Local |
|------------------------------------|---------------------------|--------------|
| [Usar gerenciadores de pacotes de R convencionais](use-r-package-managers-on-sql-server.md)  | Admin | Local |
| [Usar RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Administrador habilitado, funções de banco de dados posteriormente | both|
| [Use o T-SQL (CREATE EXTERNAL LIBRARY)](install-r-packages-tsql.md) | Administrador habilitado, funções de banco de dados posteriormente | both 

## <a name="who-installs-permissions"></a>Quem instala (permissões)

A biblioteca de pacotes de R está fisicamente localizada na pasta arquivos de programa da instância do SQL Server em uma pasta segura com acesso restrito. Gravação para este local requer permissões de administrador.

Não-administradores podem instalar pacotes, mas isso exige configuração adicional e a capacidade não está disponível em instalações inicias. Há duas abordagens para instalações de pacote de não administrador: RevoScaleR usando a versão 9.0.1 e posterior, ou usando CREATE EXTERNAL LIBRARY (apenas no SQL Server 2017). No SQL Server 2017, **dbo_owner** ou outro usuário com permissão CREATE EXTERNAL LIBRARY pode instalar pacotes R no banco de dados atual.

Os desenvolvedores do R estão acostumados a criação de bibliotecas de usuário para os pacotes que precisam se localizado centralmente as bibliotecas estão fora dos limites. Essa prática é problemática para código de R executando em uma instância do mecanismo de banco de dados do SQL Server. SQL Server não pode carregar pacotes de bibliotecas externas, mesmo se essa biblioteca está no mesmo computador. Somente os pacotes da biblioteca de instância podem ser usados no código R em execução no SQL Server.

Acesso de sistema de arquivos normalmente é restrito no servidor e, mesmo que você tenha direitos de administrador e o acesso a uma pasta de documentos do usuário no servidor, o tempo de execução do script externo que é executado no SQL Server não pode acessar todos os pacotes instalados fora da instância padrão biblioteca. 

## <a name="considerations-for-package-installation"></a>Considerações sobre a instalação do pacote

Antes de instalar novos pacotes, considere se os recursos habilitados por um determinado pacote são adequados em um ambiente do SQL Server. Em um ambiente do SQL Server protegido, você talvez queira evitar o seguinte:

+ Pacotes que exigem acesso à rede
+ Pacotes que exigem acesso de sistema de arquivos com privilégios elevados
+ Pacote é usado para desenvolvimento da web ou outras tarefas que não são beneficiadas pela execução dentro do SQL Server

## <a name="offline-installation-no-internet-access"></a>Instalação offline (sem acesso à internet)

Em geral, os servidores que hospedam os bancos de dados de produção bloqueiam conexões de internet. Instalando novos pacotes de R ou Python em tais ambientes requer que você preparar pacotes e dependências com antecedência e copie os arquivos para uma pasta no servidor para instalação offline.

Identificar todas as dependências fica complicado. Para R, é recomendável que você use [miniCRAN para criar um repositório local](create-a-local-package-repository-using-minicran.md) e, em seguida, transferir o repositório completamente definido para uma instância isolada do SQL Server.

Como alternativa, você pode executar essas etapas manualmente:

1. Identificar todas as dependências de pacote. 
2. Verifique se todos os pacotes necessários já estão instalados no servidor. Se o pacote estiver instalado, verifique se a versão correta.
3. Baixe o pacote e todas as dependências para um computador separado.
4. Mova os arquivos para uma pasta acessível pelo servidor.
5. Execute um comando de instalação com suporte ou a instrução DDL para instalar o pacote para a biblioteca de instância.

### <a name="download-the-package-as-a-zipped-file"></a>Baixe o pacote como um arquivo compactado

Para instalação em um servidor sem acesso à internet, você deve baixar uma cópia do pacote no formato de um arquivo compactado para instalação offline. **Não descompacte o pacote.**

Por exemplo, o procedimento a seguir descreve agora para obter a versão correta do [FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) pacote da Bioconductor, supondo que o computador tem acesso à internet.

1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .

2.  Clique com botão direito no link para o. Arquivo ZIP e selecione **Salvar destino como**.

3.  Navegue até a pasta local onde os pacotes compactados são armazenados e clique em **salvar**.

    Esse processo cria uma cópia local do pacote. 

4. Se você receber um erro de download, tente um site diferente do espelho.

5. Depois que tiver sido baixado o arquivo de pacote, você pode instalar o pacote ou copiar o pacote compactado para um servidor que não tem acesso à internet.

> [!TIP]
> Se por engano, você instalar o pacote em vez de baixar os binários, uma cópia do arquivo compactado baixado também é salva em seu computador. Observe as mensagens de status conforme o pacote é instalado para determinar o local do arquivo. Você pode copiar esse arquivo compactado para o servidor que não tem acesso à internet.
> 
> No entanto, quando você obter pacotes usando esse método, as dependências não são incluídas. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Instalação lado a lado com Standalone R ou Python servidores

Recursos de R e Python estão incluídos em vários produtos da Microsoft, que pode coexistir no mesmo computador.

Se você instalou o SQL Server 2017 Microsoft Machine Learning Server (autônomo) ou SQL Server 2016 R Server (autônomo), além de análise no banco de dados (SQL Server 2017 Machine Learning Services e SQL Server 2016 R Services), o computador possui separado instalações do R para cada um, com as duplicatas de todas as bibliotecas e ferramentas do R.

Pacotes que estão instalados na biblioteca R_SERVER são usados somente por um servidor autônomo e não podem ser acessados por uma instância do SQL Server (no banco de dados). Sempre use o `R_SERVICES` biblioteca ao instalar os pacotes que você deseja usar no banco de dados no SQL Server. Para obter mais informações sobre os caminhos, consulte [local da biblioteca do pacote](../package-management/default-packages.md).

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)

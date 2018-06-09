---
title: Instalar novos pacotes de R nos serviços de aprendizado de máquina do SQL Server | Microsoft Docs
description: Adicionar novos pacotes de R para SQL Server 2016 R Services ou serviços do aprendizado de máquina 2017 SQL Server (no banco de dados)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e05842a8e8a5a1d2454dbbe500b4d5aa95fca660
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707074"
---
# <a name="install-new-r-packages-on-sql-server"></a>Instalar novos pacotes de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como instalar novos pacotes de R em uma instância do SQL Server onde o aprendizado de máquina está habilitado. Há vários métodos para instalar novos pacotes de R, dependendo de qual versão do SQL Server que você tem e se o servidor tem uma conexão de internet. As seguintes abordagens para nova instalação de pacote são possíveis.

| Abordagem                           | Permissões               | Remoto/Local |
|------------------------------------|---------------------------|--------------|
| [Use gerenciadores de pacotes de R convencionais](use-r-package-managers-on-sql-server.md)  | Admin | Local |
| [Usar RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Administrador habilitada, funções de banco de dados posteriormente | both|
| [Usar o T-SQL (criar biblioteca externa)](install-r-packages-tsql.md) | Administrador habilitada, funções de banco de dados posteriormente | both 

## <a name="who-installs-permissions"></a>Quem instala (permissões)

A biblioteca de pacote de R está fisicamente localizada na pasta arquivos de programas da instância do SQL Server em uma pasta segura com acesso restrito. A gravação nesse local requer permissões de administrador.

Não-administradores podem instalar pacotes, mas isso exige configuração addititional e funcionalidade não disponível em instalações inicias. Há duas abordagens para instalações do pacote de não administrador: RevoScaleR usando a versão 9.0.1 e posterior, ou usando criar biblioteca externa (somente SQL Server 2017). No SQL Server de 2017, **dbo_owner** ou outro usuário com permissão de criar biblioteca externa pode instalar pacotes R para o banco de dados atual.

Os desenvolvedores de R estão acostumados a criar bibliotecas de usuário para os pacotes que precisam se bibliotecas centralizadas estão fora dos limites. Essa prática é problemática para o código R executado em uma instância do mecanismo de banco de dados do SQL Server. SQL Server não pode carregar pacotes de bibliotecas externas, mesmo se a biblioteca está no mesmo computador. Somente os pacotes da biblioteca de instância podem ser usados no código de R em execução no SQL Server.

Acesso de sistema de arquivos normalmente é restrito no servidor e, mesmo se você tiver direitos de administrador e o acesso a uma pasta de documentos do usuário no servidor, o tempo de execução do script externo que é executado no SQL Server não pode acessar todos os pacotes instalados fora da instância padrão biblioteca. 

## <a name="considerations-for-package-installation"></a>Considerações sobre a instalação do pacote

Antes de instalar novos pacotes, considere se os recursos habilitados por um determinado pacote são adequados em um ambiente do SQL Server. Em um ambiente protegido do SQL Server, você talvez queira evitar o seguinte:

+ Pacotes que solicitam acesso à rede
+ Pacotes que exigem Java ou outras estruturas não geralmente usadas em um ambiente do SQL Server
+ Pacotes que exigem acesso de sistema de arquivos com privilégios elevados
+ Pacote é usado para desenvolvimento na web ou outras tarefas que não se beneficiam ao ser executado dentro do SQL Server

## <a name="offline-installation-no-internet-access"></a>Instalação offline (sem acesso à internet)

Em geral, os servidores que hospedam os bancos de dados de produção bloqueiam conexões de internet. A instalação de novos pacotes de R ou Python nesses ambientes requer que você prepare pacotes e dependências com antecedência e copie os arquivos para uma pasta no servidor para instalação offline.

Identificar todas as dependências obtém complicada. Para R, é recomendável que você use [miniCRAN para criar um repositório local](create-a-local-package-repository-using-minicran.md) e, em seguida, transferir o repositório totalmente definido para uma instância do SQL Server isolada.

Também é possível executar esta etapa manualmente:

1. Identificar todas as dependências de pacote. 
2. Verifique se os pacotes necessários já estão instalados no servidor. Se o pacote estiver instalado, verifique se a versão correta.
3. Baixe o pacote e todas as dependências para um computador separado.
4. Mova os arquivos para uma pasta acessível pelo servidor.
5. Execute um comando de instalação com suporte ou uma instrução DDL para instalar o pacote para a biblioteca de instância.

### <a name="download-the-package-as-a-zipped-file"></a>Baixe o pacote como um arquivo compactado

Para instalação em um servidor sem acesso à internet, você deve baixar uma cópia do pacote no formato de um arquivo compactado para instalação offline. **Não descompacte o pacote.**

Por exemplo, o procedimento a seguir descreve agora para obter a versão correta do [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) pacote da Bioconductor, supondo que o computador tem acesso à internet.

1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .

2.  Clique no link para o. Arquivo ZIP e selecione **Salvar destino como**.

3.  Navegue até a pasta local onde os pacotes compactados são armazenados e clique em **salvar**.

    Esse processo cria uma cópia local do pacote. 

4. Se você receber um erro de download, tente um site diferente do espelho.

5. Depois que o arquivo de pacote foi baixado, você pode instalar o pacote ou copiar o pacote compactado em um servidor que não tenha acesso à internet.

> [!TIP]
> Se por engano, você instalar o pacote em vez de baixar os binários, uma cópia do arquivo compactado baixado também serão salvos em seu computador. Observe as mensagens de status que o pacote for instalado, para determinar o local do arquivo. Você pode copiar o arquivo compactado para o servidor que não tem acesso à internet.
> 
> No entanto, quando você obter pacotes usando esse método, as dependências não são incluídas. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Instalação lado a lado com Standalone R ou servidores de Python

Recursos de R e Python estão incluídos em vários produtos da Microsoft, que pode coexistir no mesmo computador.

Se você instalou o servidor SQL Server 2017 Microsoft Machine Learning (autônomo) ou o servidor do SQL Server 2016 R (autônomo) além de análise no banco de dados (serviços de aprendizado de máquina do SQL Server 2017 e SQL Server 2016 R Services), o computador tem separado instalações do R para cada um, com as duplicatas de todas as bibliotecas e ferramentas de R.

Pacotes que estão instalados para a biblioteca R_SERVER são usados somente por um servidor autônomo e não podem ser acessados por uma instância do SQL Server (no banco de dados). Use sempre o `R_SERVICES` biblioteca ao instalar os pacotes que você deseja usar no banco de dados no SQL Server. Para obter mais informações sobre os caminhos, consulte [biblioteca local do pacote](installing-and-managing-r-packages.md#package-library-location).


## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)
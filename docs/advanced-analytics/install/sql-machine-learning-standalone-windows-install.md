---
title: Instalar o servidor de aprendizado de máquina do SQL Server de 2017 (autônomo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cb906a8a05221204ec10310d652f6891861d35e2
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34708264"
---
# <a name="install-sql-server-2017-machine-learning-server-standalone-on-windows"></a>Instalar o SQL Server (autônomo) no Windows de aprendizado de máquina de servidor de 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Instalação do SQL Server inclui a opção para instalar uma servidor que executa fora do SQL Server de aprendizado de máquina. Essa opção pode ser útil se você precisa desenvolver alto desempenho aprendizado de máquina soluções que podem usar remoto contextos de computação, alternância de maneira intercambiável entre o servidor local e uma máquina de aprendizado servidor remoto em um cluster Spark ou em outro SQL Server instância.
  
Este artigo descreve como usar a instalação do SQL Server para instalar a versão autônoma do **o servidor de aprendizado de máquina do SQL Server de 2017**. 

## <a name="bkmk_prereqs"> </a> Lista de verificação de pré-instalação

2017 do SQL Server é necessária. Se você tiver o SQL Server 2016, instale o [servidor do SQL Server 2016 R (autônomo)](sql-r-standalone-windows-install.md) em vez disso.

Se você instalou uma versão anterior, como o servidor do SQL Server 2016 R (autônomo) ou Microsoft R Server, desinstale a instalação existente antes de continuar.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o Assistente de instalação para SQL Server 2017.

2. Clique o **instalação** guia e selecione **instalação novo servidor de aprendizado de máquina (autônomo)**.
    
     ![Instalar o aprendizado de máquina servidor autônomo](media/2017setup-installation-page-mlsvr.png "Iniciar instalação do aprendizado de máquina servidor autônomo")

3. Depois que a verificação de regras for concluída, aceite os termos de licenciamento do SQL Server e selecione uma nova instalação.

4. No **seleção de recursos** página, os seguintes opções já devem estar selecionadas:

    - Server (autônomo) de aprendizado de máquina da Microsoft

    - R e Python é selecionado por padrão. Você pode desmarcar qualquer idioma, mas é recomendável que você instale pelo menos um dos idiomas com suporte.

     ![Instalar o aprendizado de máquina servidor autônomo](media/2017setup-features-page-mlsvr-rpy.png "Iniciar instalação do aprendizado de máquina servidor autônomo")
    
    Todas as outras opções devem ser ignoradas. 
    
    > [!NOTE]
    > Evitar a instalação de **recursos compartilhados** se o computador já tiver instalado para análise do SQL Server no banco de dados de serviços de aprendizado de máquina. Isso cria bibliotecas duplicadas.
    > 
    > Além disso, enquanto os scripts de R ou Python em execução no SQL Server são gerenciadas pelo SQL Server, assim como para não entrar em conflito com a memória usada por outros serviços do mecanismo de banco de dados, o servidor de aprendizado de máquina autônomo não possui essas restrições e pode interferir com outras operações de banco de dados . Por fim, o acesso remoto por meio da sessão RDP, que é geralmente usado para operacionalização, geralmente está bloqueado por administradores de banco de dados.
    > 
    > Por esses motivos, geralmente recomendamos que você instale o servidor de aprendizado de máquina (autônomo) em um computador separado dos serviços de aprendizado de máquina do SQL Server.

5.  Aceite os termos de licença para baixar e instalar a componentes de aprendizado de máquina. Se você instalar ambas as linguagens, um contrato de licença separado é necessário para o Microsoft R e Python.
    
     ![Contrato de licença do Python](media/2017setup-python-license.png "contrato de licença do Python")
    
    A instalação desses componentes, e todos os pré-requisitos que possam exigir, pode levar algum tempo. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**.

6.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.

### <a name="default-installation-folders"></a>Pastas de instalação padrão

Quando você instala o R Server ou servidor de aprendizado de máquina usando a instalação do SQL Server, as bibliotecas de R são instaladas em uma pasta associada com a versão do SQL Server que você usou para a instalação. Nessa pasta, você também encontrará dados de exemplo, a documentação para os pacotes de base de R e a documentação das ferramentas de R e tempo de execução.

No entanto, se você instalar usando o Windows installer separado ou se você atualizar usando o Windows installer separado, bibliotecas de R são instaladas em uma pasta diferente.

Apenas para referência, se você instalou uma instância do SQL Server com serviços de R (no banco de dados) ou serviços de aprendizado de máquina (no banco de dados), e essa instância está no mesmo computador, as ferramentas e bibliotecas de R são instaladas por padrão em uma pasta diferente.

A tabela a seguir lista os caminhos para cada instalação.

|Versão| Método de instalação | Pasta padrão|
|----|----|----|
|Servidor de aprendizado de máquina do SQL Server de 2017 (autônomo) |  Assistente de instalação do SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Server (autônomo) de aprendizado de máquina da Microsoft |  Instalador autônomo do Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|Serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados) |Assistente de instalação do SQL Server 2017, com a opção de linguagem R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (autônomo) |  Assistente de instalação do SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (no banco de dados) |Assistente de instalação do SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

## <a name="development-tools"></a>Ferramentas de desenvolvimento

Um IDE de desenvolvimento não é instalado como parte da instalação. Ferramentas adicionais não são necessárias, como as ferramentas padrão estão incluídas que pode ser fornecida com uma distribuição de R ou Python.

É recomendável que você tente a nova versão do [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] ou [Python para Visual Studio](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio). Visual Studio oferece suporte tanto R e Python, bem como ferramentas de desenvolvimento de banco de dados, a conectividade com o SQL Server e ferramentas de BI. No entanto, você pode usar qualquer ambiente de desenvolvimento preferencial, incluindo RStudio.

## <a name="get-help"></a>Obter ajuda

Precisa de ajuda com a instalação ou atualização? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o seguinte artigo:

* [Atualização e instalação perguntas Frequentes – serviços de aprendizado de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, tente esses relatórios personalizados.

* [Relatórios personalizados do SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores de R podem começar com alguns exemplos simples e conheça os fundamentos de como funciona o R com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise de no banco de dados para os desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores de Python podem Saiba como usar o Python com o SQL Server por esses tutoriais a seguir:

+ [Tutorial: Executar Python em T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise de no banco de dados para desenvolvedores Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).

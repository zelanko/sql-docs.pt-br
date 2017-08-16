---
title: Baixar o SSDT (SQL Server Data Tools) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- instalar o ssdt, baixar o ssdt, ssdt mais recente
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: 4bcceaeca15c3fa20cd797bda0182cf48f73a730
ms.contentlocale: pt-br
ms.lasthandoff: 08/08/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>Baixar o SQL Server Data Tools (SSDT)

O **[SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)** é uma ferramenta de desenvolvimento moderna que você pode baixar gratuitamente para compilar bancos de dados relacionais do SQL Server, bancos de dados SQL do Azure, pacotes do Integration Services, modelos de dados do Analysis Services e relatórios do Reporting Services. Com o SSDT, você pode projetar e implantar qualquer tipo de conteúdo do SQL Server com a mesma facilidade com que desenvolve um aplicativo no Visual Studio. Esta versão tem suporte para o SQL Server 2017 por meio do SQL Server 2005 e fornece o ambiente de design para adicionar recursos que são novos no SQL Server.  
    
    
![download](../ssdt/media/download.png) [Baixar o SQL Server Data Tools 17.2 para Visual Studio 2015](https://go.microsoft.com/fwlink/?linkid=852922)

![download](../ssdt/media/download.png) [Baixar o DacFx (Data-Tier Application Framework) 17.2](https://www.microsoft.com/download/details.aspx?id=55713)

## <a name="sql-server-data-tools"></a>SQL Server Data Tools   
**Informações sobre versão**  
  
O número da versão: 17.2  
O número de build desta versão: 14.0.61707.300
  
**Novidades**

**AS**

- A Segurança em nível de objeto agora pode ser configurada na caixa de diálogo Funções para segurança avançada em modelos de tabelas de nível de compatibilidade 1400.
- Nova seleção de membro de função AAD para usuários sem endereços de email em modelos do AS Azure em projetos SSDT AS para VS2017.
- Nova propriedade de projeto "Sempre solicitar" do AS Azure em projetos de tabela do SSDT AS para personalizar o comportamento de armazenamento em cache de credenciais ADAL.


**Problemas conhecidos**

- Para obter uma lista completa das alterações, consulte o [log de mudanças](changelog-for-sql-server-data-tools-ssdt.md).
- Relate problemas no site de [Comentários do SSDT Connect](https://connect.microsoft.com/SQLServer/Feedback).

> [!NOTE]
> Para usar o SQL Server Data Tools no Visual Studio 2017, consulte [esta](#use-ssdt-in-visual-studio-2017) seção abaixo

  **Idiomas disponíveis**  
  
 Esta versão do SSDT pode ser instalada nos seguintes idiomas:  
[Chinês (República Popular da China)]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x804) | 
[Chinês (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x404) | 
[Inglês (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x409) | 
[Francês]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x40c)  
[Alemão]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x410) | 
[Japonês]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x412) | 
[Português (Brasil)]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x416) | 
[Russo]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x419) | 
[Espanhol]( https://go.microsoft.com/fwlink/?linkid=852922&clcid=0x40a)  

**Imagens ISO**

Uma imagem ISO do SSDT pode ser usada como uma alternativa para instalar o SSDT ou configurar um ponto de instalação administrativa. O ISO é um arquivo autossuficiente que contém todos os componentes necessários ao SSDT e pode ser baixado com um gerenciador de download reiniciável, útil para situações com pouca ou limitada largura de banda de rede. Depois de baixado, o ISO poderá ser montado como uma unidade ou gravado em um DVD.

[Chinês (República Popular da China)]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x804) |
[Chinês (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x404) |
[Inglês (Estados Unidos)]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x409) |
[Francês]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x40c)  
[Alemão]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x407) |
[Italiano]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x410) |
[Japonês]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x411) |
[Coreano]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x412) |
[Português (Brasil)]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x416) |
[Russo]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x419) |
[Espanhol]( https://go.microsoft.com/fwlink/?linkid=852942&clcid=0x40a)

## <a name="download-visual-studio"></a>Baixar o Visual Studio

* [**Baixar o Visual Studio Community 2015**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>Instalação do SSDT sem o Visual Studio pré-instalado

Se você não tiver o Visual Studio instalado em seu computador, instalar o SSDT para Visual Studio 2015 também instalará uma versão mínima do "Shell Integrado" do Visual Studio 2015. Esta versão do Visual Studio é gratuita para instalar e usar em quantos computadores quiser. Ela oferece a você todos os tipos de projeto do SQL Server, além do Pesquisador de Objetos do SQL Server e outras experiências de ferramentas do SQL.

Se você tiver o [Visual Studio 2015 Community Edition (ou superior)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) instalado em seu computador, instalar o SSDT adicionará o conjunto completo de ferramentas do SQL Server à sua instalação existente do Visual Studio. O Visual Studio inclui muitos recursos que talvez você deseje usar, como suporte a linguagens não SQL e integração do controle do código-fonte. É recomendável usar o Visual Studio 2015 Community ou superior para obter a melhor experiência ao desenvolver T-SQL.

## <a name="supported-sql-versions"></a>Versões do SQL com suporte
  
|Modelos de projeto|Plataformas SQL com suporte|  
|-------------------|--------------------|  
Bancos de dados relacionais|  SQL Server 2005* – SQL Server 2017 <br /><br />Banco de dados SQL do Azure<br /><br />SQL Data Warehouse do Azure (dá suporte somente a consultas; ainda não há suporte para projetos de banco de dados)<br /><br />  * O suporte ao SQL Server 2005 está preterido,<br /><br /> passe para uma versão do SQL oficialmente com suporte|
  |Modelos do Analysis Services<br /><br />Relatórios do Reporting Services | SQL Server 2008 – SQL Server 2017|
  |pacotes do Integration Services| SQL Server 2012 – SQL Server 2017    |
  
## <a name="next-steps"></a>Próximas etapas  
Depois de instalar o SSDT, trabalhe com esses tutoriais para aprender a criar bancos de dados, pacotes, modelos de dados e relatórios usando o SSDT:  
  
-   [Desenvolvimento de banco de dados offline orientado a projetos](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [Tutorial SSIS: Criando um pacote ETL simples](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Tutoriais do Analysis Services](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [Criando um relatório de tabela básico (Tutorial do SSRS)](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="use-ssdt-in-visual-studio-2017"></a>Usar o SSDT no Visual Studio 2017 

* [**Baixar Visual Studio 2017**](https://www.visualstudio.com/) ([comparar funcionalidades do Visual Studio 2017 por edição](https://www.visualstudio.com/vs/compare/))

Para usar os projetos de banco de dados relacional, recomendamos verificar a carga de trabalho **Armazenamento de Dados e Processamento** durante a instalação. O suporte ao projeto de banco de dados do SSDT também está incluído em várias outras cargas de trabalho, incluindo *Azure*, *ASP.Net e Desenvolvimento da Web* e *Desenvolvimento de plataforma cruzada do .Net Core*.

> [!NOTE]
> Projetos de banco de dados do SSDT no Visual Studio 2017 são compatíveis com versões até o SQL Server 2016 no momento.  O suporte para SQL Server 2017 estará disponível em breve em uma atualização do Visual Studio 2017.

Se você estiver usando o SSDT com o Visual Studio 2017, instale os componentes AS e RS:
* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="see-also"></a>Consulte também  
[SQL Server Data Tools no Visual Studio](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[Fórum do MSDN do SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog da equipe do SSDT](http://blogs.msdn.com/b/ssdt/)  
[Comentários sobre a conexão do SSDT](https://connect.microsoft.com/SQLServer/Feedback)  
[Documentação do SSDT](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[Referência DACFx API](https://msdn.microsoft.com/library/dn645454.aspx)  
[Baixar o SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  


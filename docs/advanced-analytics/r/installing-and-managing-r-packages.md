---
title: Instalar e gerenciar pacotes do R | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae30bfc42e42b69158dbba5a38b0bccbe93523b4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="installing-and-managing-r-packages"></a>Instalar e gerenciar pacotes do R
 Qualquer solução de R que seja executada em [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] deve usar pacotes instalados na biblioteca padrão do R. Normalmente, as soluções de R farão referência a bibliotecas do usuário por meio da especificação de um caminho de arquivo no código R, mas isso não é recomendado para produção.

Portanto, é tarefa de administrador do banco de dados ou outro administrador no servidor assegurar que todos os pacotes necessários sejam instalados na instância [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Se você não tiver privilégios administrativos no computador que hospedar a instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], você poderá fornecer as informações do administrador sobre como instalar pacotes do R e fornecer acesso a um repositório de pacote seguro em que os pacotes solicitados pelos usuários possam ser obtidos. Esta seção fornece essas informações. 

> [!TIP]
> O [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] fornece novos recursos para instalar e gerenciar pacotes do R que oferecem maior liberdade e controle sobre instalação e uso do pacote, tanto ao administrador de banco de dados quanto ao cientista de dados. Para obter mais informações, consulte [Gerenciamento de pacotes do R para o SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

## <a name="installed-packages"></a>Pacotes instalados
Quando você instala os [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], os pacotes **básicos** do R como `stats` e `utils` são instalados por padrão, juntamente com o pacote **RevoScaleR** que dá suporte a conexões com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
> [!NOTE]  
>  Para obter uma lista de pacotes instalados por padrão, consulte [Pacotes instalados com o Microsoft R Open](https://mran.microsoft.com/rro/installed/).  

 Se você precisar de um pacote adicional do CRAN ou outro repositório, será necessário baixar o pacote e instalá-lo em sua estação de trabalho.  
  
 Se você precisar executar o novo pacote no contexto do servidor, será necessário também que um administrador o instale no servidor.   
   
## <a name="where-and-how-to-get-new-packages"></a>Onde e como obter novos pacotes  
 Há várias fontes de pacotes R, os mais conhecidos entre eles são CRAN e Bioconductor. O site oficial da linguagem R ([https://www.r-project.org/](https://www.r-project.org/)) lista vários desses recursos. Muitos pacotes também são publicados no GitHub, onde é possível obter o código-fonte. No entanto, talvez você também tenha recebido pacotes R desenvolvidos por alguém de sua empresa.  
  
 Independentemente da origem, os pacotes devem ser fornecidos no formato de um arquivo compactado para ser instalado. Além disso, para usar o pacote com os [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], certifique-se de obter o arquivo compactado no formato binário do Windows. (Alguns pacotes podem não dar suporte a esse formato.) Para obter mais informações sobre o conteúdo do formato de arquivo zip e como criar um pacote do R, recomendamos este tutorial, que pode ser baixado no formato PDF no site do projeto do R: [Freidrich Leisch: criação de pacotes do R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf). 
  
 Em geral, se o computador tiver acesso à Internet, os pacotes do R poderão ser instalados facilmente da linha de comando sem que precisem ser previamente baixados.  Geralmente esse não é o caso com servidores que executam o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  Portanto, para instalar o pacote do R em um computador **sem** acesso à Internet, será necessário baixar o pacote antecipadamente no formato compactado correto e, em seguida, copiar os arquivos compactados em uma pasta que possa ser acessada pelo computador. 
 
 Os tópicos a seguir descrevem os dois métodos para instalar pacotes offline: 

+ [Criar um repositório de pacote offline usando o miniCRAN](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  Descreve como usar o pacote do R **miniCRAN** para criar um repositório offline. Esse é provavelmente o método mais eficiente se você precisa instalar os pacotes em vários servidores e gerenciar o repositório de um único local. 
+ [Instalar novos pacotes do R da Internet](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  Inclui instruções para instalar os pacotes offline copiando manualmente os arquivos compactados.   

## <a name="permissions-required-for-installing-r-packages"></a>Permissões necessárias para instalar pacotes de R  
  
Para instalar um novo pacote do R em um computador que está executando o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você precisa ter direitos administrativos no computador.   

Se você não tiver esses direitos, entre em contato com o administrador e forneça as informações sobre o pacote para instalação.  
  

Se você estiver instalando um novo pacote do R em um computador que está sendo usado como uma estação de trabalho de R e o computador **não** tiver uma instância de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instalada, você ainda precisará de direitos administrativos no computador para instalar o pacote. Após a instalação do pacote, você pode executá-lo localmente.  
 
> [!NOTE]
> Em [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], novas funções de banco de dados foram adicionadas para dar suporte a escopo de permissões de instalação do pacote em um nível de instância e um nível de banco de dados. Para obter mais informações, consulte [Gerenciamento de pacotes do R para o SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 

### <a name="location-of-default-r-library-location-for-r-services"></a>Local da biblioteca padrão do R para o R Services

Se você instalou os [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usando a instância padrão, a biblioteca de pacotes do R usada pela instância está localizada na pasta da instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Por exemplo: 

+ Instância padrão _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ Instância nomeada _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


Você pode executar a instrução a seguir para verificar a biblioteca padrão para a instância atual do R. 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

Para obter mais informações, consulte [Determinar quais pacotes estão instalados no SQL Server](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md).

## <a name="managing-installed-packages"></a>Gerenciar pacotes instalados

O [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] fornece novos recursos para instalar e gerenciar pacotes do R que oferecem maior liberdade e controle sobre instalação e uso do pacote, tanto ao administrador de banco de dados quanto ao cientista de dados. Para obter mais informações, consulte [Gerenciamento de pacotes do R para o SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

Se você está usando o SQL Server 2106 R Services, os novos recursos de gerenciamento de pacotes não estão disponíveis no momento. Enquanto isso, para determinar quais pacotes estão instalados no computador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], use uma das seguintes opções:

+ Exiba a biblioteca padrão, se você tiver permissões para a pasta.
+ Execute um comando do R para listar os pacotes no local de biblioteca R_SERVICES
+ Use um procedimento armazenado como o seguinte na instância:
   ```SQL
   EXECUTE sp_execute_external_script  @language=N'R'  
        ,@script = N'str(OutputDataSet);  
        packagematrix <- installed.packages();  
        NameOnly <- packagematrix[,1];  
        OutputDataSet <- as.data.frame(NameOnly);'  
        ,@input_data_1 = N'SELECT 1 as col'  
        WITH RESULT SETS ((PackageName nvarchar(250) ))   
   ```


 ## <a name="see-also"></a>Consulte também  
 [Gerenciando e monitorando soluções de R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  


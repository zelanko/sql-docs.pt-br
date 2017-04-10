---
title: "Instalar e gerenciar pacotes de R | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Instalar e gerenciar pacotes de R
 Qualquer solução de R que é executado em [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] deve usar pacotes que estão instalados na biblioteca padrão R. Normalmente, as soluções R fará referência a bibliotecas do usuário, especificando um caminho de arquivo no código R, mas isso não é recomendado para produção.

Portanto, é a tarefa de administrador do banco de dados ou outro administrador no servidor para garantir que todos os pacotes necessários são instalados na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância. Se você não tem privilégios administrativos no computador que hospeda o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]  instância, você pode fornecer as informações do administrador sobre como instalar pacotes de R e fornecer acesso a um repositório de pacote seguro onde os pacotes solicitados pelos usuários podem ser obtidos. Esta seção fornece essas informações. 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] fornece novos recursos para instalar e gerenciar pacotes de R que oferecem tanto o administrador de banco de dados e os dados cientista maior liberdade e controle sobre instalação e uso do pacote. Para obter mais informações, consulte [R pacote de gerenciamento para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

## <a name="installed-packages"></a>Pacotes instalados
Quando você instala o  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)],  por padrão o R **base** pacotes são instalados, como `stats` e `utils`, juntamente com o **RevoScaleR** pacote que oferece suporte a conexões com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
> [!NOTE]  
>  Para obter uma lista de pacotes instalados por padrão, consulte [pacotes instalados com o Microsoft R Open](https://mran.microsoft.com/rro/installed/).  

 Se você precisar de um pacote adicional de CRAN ou outro repositório, você deve baixar o pacote e instalá-lo em sua estação de trabalho.  
  
 Se você precisar executar o novo pacote no contexto do servidor, um administrador deve instalá-lo no servidor.   
   
## <a name="where-and-how-to-get-new-packages"></a>Onde e como obter novos pacotes  
 Há várias fontes de pacotes R, os mais conhecidos entre eles são CRAN e Bioconductor. O site oficial da linguagem R ([https://www.r-project.org/](https://www.r-project.org/)) lista vários desses recursos. Muitos pacotes também são publicados no GitHub, onde é possível obter o código-fonte. No entanto, talvez você também tenha recebido pacotes R desenvolvidos por alguém de sua empresa.  
  
 Independentemente da origem, os pacotes devem ser fornecidos no formato de um arquivo compactado para ser instalado. Além disso, para usar o pacote com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], certifique-se de obter o arquivo compactado no formato binário do Windows. (Alguns pacotes podem não suportar esse formato.) Para obter mais informações sobre o conteúdo do formato de arquivo zip e como criar um pacote R, recomendamos que este tutorial, o que pode ser baixado no formato PDF no site do projeto R: [Freidrich Leisch: criação de pacotes de R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf). 
  
 Em geral, pacotes R podem ser instalados facilmente na linha de comando sem baixá-los de antemão, se o computador tiver acesso à Internet.  Geralmente isso não é o caso com servidores que executam o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] .  Portanto, para instalar um pacote R em um computador que faz **não** ter acesso à Internet, você deve baixar o pacote no formato compactado correto antecipadamente e, em seguida, copie os arquivos compactados para uma pasta que possa ser acessada pelo computador. 
 
 Os tópicos a seguir descrevem os dois métodos para instalar pacotes offline: 

+ [Criar um repositório de pacote Offline usando miniCRAN](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  Descreve como usar o pacote R **miniCRAN** para criar um repositório offline. Isso provavelmente é o método mais eficiente se você precisa instalar os pacotes para vários servidores e gerenciar o repositório de um único local. 
+ [Instalar novos pacotes de R da Internet](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  Inclui instruções para instalar os pacotes offline copiando manualmente os arquivos compactados.   

## <a name="permissions-required-for-installing-r-packages"></a>Permissões necessárias para instalar pacotes de R  
  
Para instalar um novo pacote de R em um computador que está executando o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você precisa ter direitos administrativos no computador.   

Se você não tiver esses direitos, entre em contato com o administrador e forneça as informações sobre o pacote para instalação.  
  

Se você estiver instalando um novo pacote de R em um computador que está sendo usado como uma estação de trabalho de R e o computador não **não** tiver uma instância de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instalado, você ainda precisa de direitos administrativos no computador para instalar o pacote. Após a instalação do pacote, você pode executá-lo localmente.  
 
> [!NOTE]
> Em [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], novas funções de banco de dados foram adicionadas para oferecer suporte a escopo de permissões de instalação do pacote em um nível de instância e nível de banco de dados. Para obter mais informações, consulte [R pacote de gerenciamento para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 

### <a name="location-of-default-r-library-location-for-r-services"></a>Local de biblioteca padrão R para serviços de R

Se você instalou o  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usando a instância padrão, a biblioteca de pacote de R usada pela instância está localizada sob o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pasta da instância. Por exemplo: 

+ Instância padrão _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ Instância nomeada _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


Você pode executar a instrução a seguir para verificar se a biblioteca padrão para a instância atual de R. 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

Para obter mais informações, consulte [determinar quais pacotes estão instalados no servidor SQL](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md).

## <a name="managing-installed-packages"></a>Gerenciando pacotes instalados

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] fornece novos recursos para instalar e gerenciar pacotes de R que oferecem tanto o administrador de banco de dados e os dados cientista maior liberdade e controle sobre instalação e uso do pacote. Para obter mais informações, consulte [R pacote de gerenciamento para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

Se você estiver usando os serviços do SQL Server 2106 R, os novos recursos de gerenciamento de pacote não estão disponíveis no momento. Enquanto isso, você tem estas opções para determinar quais pacotes estão instalados no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador, use uma das seguintes opções:

+ Exiba a biblioteca padrão, se você tiver permissões para a pasta.
+ Executar um comando do comando de R para listar os pacotes no local de biblioteca R_SERVICES
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
 [Gerenciar e monitorar soluções R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
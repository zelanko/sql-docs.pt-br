---
title: Serviços de mineração de dados e fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b26fd6e3-7d87-4f66-ab47-5303b51b87da
author: minewiskan
ms.author: owend
ms.openlocfilehash: afba038563ec5934a874811c804dd7a4aa9fff1e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523072"
---
# <a name="data-mining-services-and-data-sources"></a>Serviços de mineração de dados e fontes de dados
  A mineração de dados requer uma conexão com uma instância do SQL Server Analysis Services. Os dados de um cubo não são necessários para a mineração de dados e o uso de fontes relacionais é recomendado; porém, a mineração de dados usa componentes fornecidos pelo mecanismo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Este tópico contém informações que você deverá saber quando se conectar a uma instância do SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para criar, processar, implantar ou consultar modelos de mineração de dados.  
  
## <a name="data-mining-services"></a>Serviços de mineração de dados  
 O componente de servidor do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é o msmdsrv.exe aplicativo, que normalmente é executado como um serviço do Windows. Esse aplicativo consiste em componentes de segurança, um componente de ouvinte do XML for Analysis (XMLA), um componente de processador de consulta e vários outros componentes internos que executam as seguintes funções:  
  
-   Análise de instruções recebidas dos clientes  
  
-   Gerenciamento de metadados  
  
-   Tratamento de transações  
  
-   Processamento de cálculos  
  
-   Armazenagem de dimensões e dados de célula  
  
-   Criação de agregações  
  
-   Programação de consultas  
  
-   Cache de objetos  
  
-   Gerenciamento de recursos do servidor  
  
### <a name="xmla-listener"></a>Ouvinte XMLA  
 O componente ouvinte XMLA processa todas as comunicações de XMLA entre o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e seus clientes. A [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] `Port` definição de configuração no arquivo de msmdsrv.ini pode ser usada para especificar uma porta na qual uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância escuta. Um valor 0 nesse arquivo indica que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ouve na porta padrão. A menos que especificado de outro modo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa as seguintes portas TCP padrão:  
  
|Porta|Descrição|  
|----------|-----------------|  
|2383|Instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|2382|Redirecionador para outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Atribuído dinamicamente na inicialização do servidor|Instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
 Para obter mais informações sobre como controlar as portas usadas por esse serviço, consulte [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
## <a name="connecting-to-data-sources"></a>Conectando-se a fontes de dados  
 Sempre que você criar ou atualizar uma estrutura ou um modelo de mineração de dados, use os dados definidos por uma fonte de dados. A fonte de dados não contém os dados, que podem incluir pastas de trabalho do Excel, arquivos de texto e bancos de dados do SQL Server; ela somente define as informações de conexão.  Uma exibição da fonte de dados (DSV) serve como uma camada de abstração dessa fonte, modificando ou mapeando os dados que são obtidos da fonte.  
  
 Está além do escopo deste tópico descrever os requisitos de conexão para cada uma destas fontes. Para obter mais informações, consulte a documentação do provedor. No entanto, em geral você deveria estar atento aos seguintes requisitos do Analysis Services ao interagir com provedores:  
  
-   Como a mineração de dados é um serviço fornecido por um servidor, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve receber acesso à fonte de dados.  Há dois aspectos para acessar: local e identidade.  
  
     **Local** significa que, se você criar um modelo usando dados que estão armazenados somente em seu computador e, em seguida, implantar o modelo em um servidor, o modelo não será processado porque a fonte de dados não poderá ser localizada. Para resolver este problema, você pode precisar transferir dados para a mesma instância do SQL Server onde o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] está sendo executado, ou mover os arquivos para um local compartilhado.  
  
     **Identidade** significa que os serviços no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] podem abrir o arquivo de dados ou fonte de dados com as credenciais apropriadas. Por exemplo, quando você criou o modelo, pode ter tido permissões ilimitadas para exibir os dados, mas o usuário que está processando e atualizando os modelos no servidor pode ter acesso limitado ou nenhum aos dados, o que pode causar falha ao processar ou afetar o conteúdo de um modelo. No mínimo, a conta usada para conectar-se à fonte de dados remotos deve ter permissões de leitura dos dados.  
  
-   Quando você move um modelo, os mesmos requisitos se aplicam: você deve configurar o acesso apropriado ao local da fonte de dados antiga, copiar as fontes de dados ou configurar uma nova fonte de dados. Além disso, você deve transferir logons e funções ou configurar permissões para permitir que os objetos de mineração de dados sejam processados e atualizados no novo local.  
  
## <a name="configuring-permissions-and-server-properties"></a>Configurando permissões e propriedades do servidor  
 A mineração de dados exige permissões adicionais em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . A maioria das propriedades de mineração de dados pode ser definida usando a [Caixa de diálogo Propriedades do Analysis Services &#40;Analysis Services&#41;](../analysis-server-properties-dialog-box-analysis-services.md).  
  
 Para obter mais informações sobre as propriedades que podem ser configuradas, consulte [Configure Server Properties in Analysis Services](../server-properties/server-properties-in-analysis-services.md).  
  
 As seguintes propriedades de servidor são de relevância específica para a mineração de dados:  
  
-   `AllowAdHocOpenRowsetQueries`Controla o acesso ad hoc a provedores de OLE DB, que são carregados diretamente no espaço de memória do servidor.  
  
    > [!IMPORTANT]  
    >  Para melhorar a segurança, é recomendável definir esta propriedade como `false`. O valor padrão é `false`. No entanto, ainda que esta propriedade seja definida como `false`, os usuários podem continuar criando consultas singleton e usar OPENQUERY em fontes de dados permitidas.  
  
-   **AllowedProvidersInOpenRowset** Especificará o provedor se ad hoc acesso estiver habilitado. Para especificar vários provedores, digite uma lista de ProgIDs separados por vírgula.  
  
-   **MaxConcurrentPredictionQueries** Controla a carga no servidor gerada por previsões. O valor padrão de 0 permite consultas ilimitadas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise e no máximo cinco consultas simultâneas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard. As consultas que ultrapassam o limite são serializadas e podem expirar.  
  
 O servidor oferece outras propriedades que controlam quais algoritmos de mineração de dados ficam disponíveis, inclusive todas as restrições sobre algoritmos, e os padrões para serviços de mineração de dados. Porém, não há configurações que permitem controlar especificamente o acesso a procedimentos armazenados de mineração de dados. Para obter mais informações, consulte [Propriedades de Data Mining](../server-properties/data-mining-properties.md).  
  
 Também é possível definir propriedades que permitem ajustar o servidor e controlar a segurança para uso de cliente. Para obter mais informações, consulte [Propriedades do Recurso](../server-properties/feature-properties.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o suporte para algoritmos de plug-in nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) ( https://go.microsoft.com/fwlink/?linkid=232473) .  
  
## <a name="programmatic-access-to-data-mining-objects"></a>Acesso programático a objetos de mineração de dados  
 Você pode usar os seguintes modelos de objeto para criar uma conexão com um banco de dados do Analysis Services e trabalhar com objetos de mineração de dados:  
  
 **ADO** Usa OLE DB para se conectar a um servidor do Analysis Services. Quando você usa ADO, o cliente fica limitado a consultas de conjunto de linhas de esquema e instruções DMX.  
  
 **ADO.NET** Interage com provedores SQL Server melhor do que outros provedores. Usa adaptadores de dados para armazenar conjuntos de linhas dinâmicos. Usa o objeto de conjunto de dados, que consiste em um cache dos dados de servidor armazenados como tabelas de dados que podem ser atualizadas e salvas como XML.  
  
 **ADOMD.NET** Um provedor de dados gerenciado que é otimizado para funcionar com mineração de dados e OLAP. O ADOMD.NET é mais rápido e faz uso mais eficiente da memória do que o ADO.NET. O ADOMD.NET também permite recuperar metadados sobre objetos de servidor. Recomendado para aplicativos cliente, exceto quando .NET não está disponível.  
  
 **ADOMD de servidor** Modelo de objeto usado para acessar objetos do Analysis Services diretamente no servidor. É utilizado por procedimentos armazenados do Analysis Services; não indicado para uso de cliente.  
  
 **AMO** Interface de gerenciamento para o Analysis Services que substitui o DSO (Decision Support Objects). Quando se usa o AMO, operações como iteração de objetos requerem permissões mais elevadas do que as necessárias para utilizar outras interfaces. Isso ocorre porque o AMO acessa metadados diretamente, enquanto o ADOMD.NET e outras interfaces acessam apenas os esquemas de banco de dados.  
  
### <a name="browse-and-query-access-to-servers"></a>Navegue e consulte o acesso a servidores  
 Você pode executar todos os tipos de previsões usando uma instância do Analysis Services no OLAP/Mineração de Dados, com as restrições a seguir:  
  
-   Se você usar ADOMD de servidor, poderá usar DMX para acessar o servidor sem fazer uma conexão. Você pode copiar os resultados diretamente para uma tabela de dados. No entanto, você não pode usar ADOMD de servidor com instâncias remotas; só é possível consultar o servidor local.  
  
-   O ADO.NET não dá suporte a parâmetros nomeados para mineração de dados. Você deve usar ADOMD.NET.  
  
-   O ADOMD.NET permite passar uma tabela inteira a ser usada como parâmetro; por isso você pode usar dados no cliente ou dados que estão indisponíveis para o servidor. Também é possível utilizar tabelas amoldadas como entrada de previsão.  
  
### <a name="using-data-mining-stored-procedures"></a>Usando procedimentos armazenados de mineração de dados  
 Um uso comum de procedimentos armazenados é o encapsulamento de consultas para reutilização. O cliente pode usar CALL para executar procedimentos armazenados, inclusive procedimentos armazenados do sistema do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Se o procedimento retornar um conjunto de dados, o cliente receberá um conjunto de dados ou uma tabela de dados com uma tabela aninhada contendo as linhas. Por exemplo, se você criar uma consulta baseada no conteúdo de modelo, a consulta retornará o modelo inteiro. Para evitar que sejam retornadas muitas linhas, você pode gravar procedimentos armazenados usando o modelo de objeto ADOMD+.  
  
 Para gravar um procedimento armazenado de servidor, você deve fazer referência ao namespace Microsoft.AnalysisServices.AdomdServer. Para obter mais informações sobre como criar e usar procedimentos armazenados, consulte [Funções e procedimentos armazenados definidos pelo usuário](https://docs.microsoft.com/analysis-services/adomd/multidimensional-models-adomd-net-server/user-defined-functions-and-stored-procedures).  
  
> [!NOTE]  
>  Os procedimentos armazenados não podem ser usados para alterar a segurança em objetos de servidor de dados. Quando você executa um procedimento armazenado, o contexto atual do usuário é usado para determinar o acesso a todos os objetos de servidor. Portanto, os usuários devem ter as permissões apropriadas em qualquer objeto de banco de dados que eles acessam.  
  
## <a name="see-also"></a>Consulte Também  
 [Arquitetura física &#40;Analysis Services de dados multidimensionais&#41;](../multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)   
 [Arquitetura física &#40;Analysis Services&#41;de mineração de dados](physical-architecture-analysis-services-data-mining.md)   
 [Gerenciamento de soluções de mineração de dados e objetos](management-of-data-mining-solutions-and-objects.md)  
  
  

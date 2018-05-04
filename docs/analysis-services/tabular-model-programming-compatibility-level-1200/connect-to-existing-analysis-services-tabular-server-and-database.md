---
title: Conecte-se ao servidor de tabela do Analysis Services existente e o banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 05be704e-4ee4-4101-b5ce-96fdda18c639
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 05b577c5ea50c6c9749221ad9d2f352b970ba62d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>Conecte-se ao banco de dados e servidor de tabela do Analysis Services existente
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
No SQL Server 2016, o Analysis Services Management Objects (AMO) inclui vários namespaces que pode ser usados para configurar uma conexão de servidor. Este artigo explica como estabelecer uma conexão de servidor usando o namespace AnalysisServices para modelos e bancos de dados criados em 1200 ou maior nível de compatibilidade. 

Para se conectar a um servidor do Analysis Services, seu código deve instanciar um objeto de servidor e, em seguida, chamar o método Connect. Uma vez conectado, propriedades do objeto Server refletirão as configurações da instância do Analysis Services atual. 

As classes a seguir podem ser usadas para conexões de nível superior: 

* Microsoft 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

Como você pode ver, dois namespaces fornecem conectividade a objetos de servidor e banco de dados: o namespace Microsoft. AnalysisServices original AMO e o novo namespace AnalysisServices para TOM.

Por que dois namespaces para as mesmas operações? A resposta está downstream, no banco de dados e o modelo de nível, onde a hierarquia de objeto se torna específicos do modo e a árvore de modelo é composta de metadados Multidimensional ou Tabular. Para fazer chamadas na árvore de modelo, o objeto de servidor ou banco de dados é fornecido para ambos os tipos de modelo.

> [!NOTE]  
>  Os metadados usados para operações e a definição do modelo são completamente diferente para os dois modos. Separando a linguagem de definição de dados (DDL) em dois namespaces separados, a experiência de desenvolvimento é simplificada por meio da apresentação da API necessária para um tipo de modelo específico. 

Embora o DDL difere, conexões com um servidor são os mesmos em todos os modos, versões e edições. Dando suporte a um servidor e a conexão de banco de dados por meio de qualquer namespace permite que você escreva ferramentas genéricas ou script que se conectar a qualquer instância do Analysis Services ou o banco de dados, sem precisar saber que tipo de modelo é hospedado no servidor.  

Essa flexibilidade explica as dependências entre os assemblies. Para fazer chamadas abaixo do nível de banco de dados (por exemplo, um modelo em um banco de dados de tabela 1200, ou em um cubo, dimensão ou MeasureGroup dentro de um banco de dados de 1050-1103 Multidimensional ou Tabular), o AMO tem uma dependência no TOM. 

Em contraste, o TOM não tem dependência no AMO. Embora o TOM não pode ser usado para explorar metadados multidimensionais (cubos), o AMO pode ser usado para explorar Multidimensional e metadados de tabela. 

Por esse motivo, a primeira etapa na configuração de seu projeto requer a adição de referências a todos os assemblies do AMO. Consulte [instalar, referência e distribuir a biblioteca de cliente de TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) para obter detalhes. 

> [!NOTE]  
>  Conexões de servidor e banco de dados são baseados em classes AMO herdadas que herdam de MajorObject. Embora os objetos principais e secundários não são usados em uma árvore de modelo de tabela, a classe MajorObject está visível como uma classe base para objetos de servidor e banco de dados, independentemente de qual API permite configurar a conexão.  

## <a name="code-example-server-connection"></a>Exemplo de código: conexão de servidor 

Abaixo está um exemplo de código c# que mostra como se conectar a uma instância local do Analysis Services e lista suas propriedades na janela do console. 

Este exemplo mostra apenas algumas das propriedades de um objeto de servidor, mas há mais propriedades disponíveis, incluindo ServerMode e DefaultCompatibilityLevel.  

```
using System; 
using Microsoft.AnalysisServices.Tabular; 

namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 


            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 

 
                Console.WriteLine("Connection established successfully."); 
                Console.WriteLine(); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.WriteLine("Server name:\t\t{0}", server.Name); 
                Console.WriteLine("Server product name:\t{0}", server.ProductName); 
                Console.WriteLine("Server product level:\t{0}", server.ProductLevel); 
                Console.WriteLine("Server version:\t\t{0}", server.Version); 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```
Quando você executa o programa, a saída mostra propriedades no objeto de servidor em uma janela de console. 

## <a name="authentication-and-authorization"></a>Autenticação e autorização 

Um servidor ou a conexão de banco de dados para o Analysis Services requer permissões administrativas, usadas para operações de leitura-gravação e passando por meio de uma solicitação de conexão representado.  

Embora a infraestrutura de segurança do Analysis Services tiver sido estendida nos últimos anos, para permitir a autenticação personalizada em condições muito específicas, o método de autenticação externa com suporte apenas é segurança integrada do Windows. Entidades de segurança devem para ser válidos domínio usuário ou grupo de contas do Windows.  

No Windows 2012 e versões posteriores, a delegação pode fluir entre domínios. No Analysis Services, a delegação é usada apenas para modelos DirectQuery. Caso contrário, as conexões são representadas ou direta. 

## <a name="next-steps"></a>Próximas etapas 

Depois de estabelecer uma conexão, a próxima etapa lógica é para qualquer um dos bancos de dados existentes de lista já no servidor, ou talvez criar um novo banco de dados vazio. Os links a seguir incluem exemplos de código que demonstram ambas as tarefas básicas: 

- [Criar e implantar um banco de dados vazio](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [Lista de bancos de dados existentes](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)

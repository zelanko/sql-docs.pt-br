---
title: Conectar-se ao banco de dados e servidor de tabela do Analysis Services existente | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13900e4aaad52d39a2691fb40d0e419f55f660fc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033386"
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>Conectar-se ao banco de dados e servidor de tabela do Analysis Services existente
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
No SQL Server 2016, o gerenciamento de objetos AMO (Analysis Services) inclui vários namespaces que pode ser usados para configurar uma conexão de servidor. Este artigo explica como estabelecer uma conexão de servidor usando o namespace AnalysisServices para modelos e bancos de dados criados em 1200 ou nível de compatibilidade mais alto. 

Para se conectar a um servidor do Analysis Services, seu código deve instanciar um objeto de servidor e, em seguida, chamar o método Connect. Uma vez conectado, as propriedades do objeto de servidor refletirão as configurações da instância do Analysis Services atual. 

As classes a seguir podem ser usadas para conexões de nível superior: 

* AnalysisServices 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

Como você pode ver, os dois namespaces fornecem conectividade a objetos de servidor e banco de dados: o namespace Microsoft. AnalysisServices original para o AMO e o novo namespace AnalysisServices para TOM.

Por que dois namespaces para as mesmas operações? A resposta está downstream, no banco de dados e o modelo de nível, em que a hierarquia de objeto se torna específicos do modo e a árvore de modelo é composta de metadados Multidimensional ou Tabular. Para fazer chamadas na árvore de modelo, o objeto de servidor ou banco de dados é fornecido para ambos os tipos de modelo.

> [!NOTE]  
>  Os metadados usados para operações e a definição do modelo são completamente diferente para os dois modos. Separando a linguagem de definição de dados (DDL) em dois namespaces separados, a experiência de desenvolvimento é simplificada por meio da apresentação da API necessária para um tipo de modelo específico. 

Embora o DDL for diferente, as conexões a um servidor são os mesmos em todos os modos, versões e edições. Suporte a um servidor e a conexão de banco de dados por meio de qualquer namespace permite que você escreva ferramentas genéricas ou script que se conectam a qualquer instância do Analysis Services ou banco de dados, sem precisar saber que tipo de modelo é hospedado no servidor.  

Essa flexibilidade explica as dependências entre os assemblies. Para fazer chamadas abaixo do nível de banco de dados (por exemplo, em um modelo dentro de um banco de dados de tabela 1200, ou em um cubo, dimensão ou MeasureGroup dentro de um banco de dados de 1050-1103 Multidimensional ou Tabular), o AMO tem uma dependência em TOM. 

Em contraste, TOM não tem dependência no AMO. Embora o TOM não pode ser usado para explorar os metadados multidimensionais (cubos), o AMO pode ser usado para explorar Multidimensional e metadados de tabela. 

Por esse motivo, a primeira etapa na configuração de seu projeto requer a adição de referências a todos os assemblies do AMO. Ver [instalar, referência e distribui a biblioteca de cliente de TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) para obter detalhes. 

> [!NOTE]  
>  Conexões de servidor e banco de dados são baseadas em classes AMO herdadas que herdam de MajorObject. Embora os objetos principais e secundárias não são usados em uma árvore de modelo de tabela, a classe MajorObject está visível como uma classe base para objetos de servidor e banco de dados, independentemente de qual API você usa para configurar a conexão.  

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
Quando você executa esse programa, a saída mostra as propriedades no objeto do servidor em uma janela do console. 

## <a name="authentication-and-authorization"></a>Autenticação e autorização 

Um servidor ou conexão de banco de dados para o Analysis Services exige permissões administrativas, usadas para operações de leitura / gravação e passar por meio de uma solicitação de conexão representado.  

Embora a infra-estrutura de segurança do Analysis Services foi estendida nos últimos anos para permitir a autenticação personalizada em condições muito específicas, o método externo com suporte somente a autenticação é segurança integrada do Windows. Entidades de segurança devem para ser válidos Windows usuário ou grupo de contas de domínio.  

No Windows 2012 e versões posteriores, a delegação pode fluir entre domínios. No Analysis Services, a delegação é usada apenas para modelos DirectQuery. Caso contrário, as conexões são diretos ou delegadas. 

## <a name="next-steps"></a>Próximas etapas 

Depois de estabelecer uma conexão, a próxima etapa lógica é qualquer um dos bancos de dados existentes de lista existente no servidor, ou talvez criar um novo banco de dados vazio. Os links a seguir incluem exemplos de código que demonstram a ambas as tarefas básicas: 

- [Criar e implantar um banco de dados vazio](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [Listar bancos de dados existentes](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)

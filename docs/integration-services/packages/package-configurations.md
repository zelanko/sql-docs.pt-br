---
title: "Configura&#231;&#245;es de pacote | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sintaxe de configuração de pacote [Integration Services]"
  - "pacotes do SQL Server Integration Services, configurações"
  - "pacotes do SSIS, configurações"
  - "XML [Integration Services]"
  - "pacotes do Integration Services, configurações"
  - "sintaxe de configuração [Integration Services]"
  - "configurações indiretas [Integration Services]"
  - "configurações [Integration Services]"
  - "configurações diretas [Integration Services]"
  - "pacotes [Integration Services], configurações"
ms.assetid: d20e0311-1fc9-4ddc-a381-6d127cf11b69
caps.latest.revision: 49
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 49
---
# Configura&#231;&#245;es de pacote
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece configurações de pacote que podem ser usadas para atualizar os valores das propriedades em tempo de execução.  
  
> **OBSERVAÇÃO:** as configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 Uma configuração é um par propriedade/valor que você adiciona a um pacote concluído. Normalmente, você cria uma definição de propriedades do pacote nos objetos do pacote durante o desenvolvimento do pacote e, depois, adiciona as configurações ao pacote. Quando o pacote é executado, obtém os novos valores da propriedade da configuração. Por exemplo, ao usar uma configuração, você pode alterar a cadeia de caracteres de conexão de um gerenciador de conexões ou atualizar o valor de uma variável.  
  
 As configurações de pacote fornecem os seguintes benefícios:  
  
-   As configurações facilitam a movimentação dos pacotes de um ambiente de desenvolvimento para um ambiente de produção. Por exemplo, uma configuração pode atualizar o caminho de um arquivo de origem, ou alterar o nome de um banco de dados ou de um servidor.  
  
-   As configurações são úteis quando você implanta pacotes em muitos servidores diferentes. Por exemplo, uma variável na configuração de cada pacote implantado pode conter um valor de espaço de disco diferente e, se o espaço em disco disponível não atingir esse valor, o pacote não será executado.  
  
-   As configurações tornam os pacotes mais flexíveis. Por exemplo, uma configuração pode atualizar o valor de uma variável usada em uma expressão de propriedade.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oferece suporte a vários métodos diferentes de armazenamento de configurações de pacote, como arquivos XML, tabelas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e variáveis de ambiente e pacote.  
  
 Cada configuração é um par propriedade/valor. O arquivo de configuração XML e os tipos de configuração [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem incluir várias configurações.  
  
 As configurações são incluídas quando você cria um utilitário de desenvolvimento de pacote para instalar pacotes. Quando você instala os pacotes, as configurações podem ser atualizadas como uma etapa na instalação de pacotes.  
  
## Compreendendo como as configurações de pacote são aplicadas em tempo de execução  
 Quando você usa o utilitário do prompt de comando **dtexec** para executar um pacote implantado, o utilitário aplica as configurações do pacote duas vezes. O utilitário aplica configurações antes e depois de aplicar as opções que você especificou na linha de comando.  
  
 Como o utilitário carrega e executa o pacote, os eventos ocorrem na seguinte ordem:  
  
1.  O utilitário **dtexec** carrega o pacote.  
  
2.  O utilitário aplica as configurações que foram especificadas no pacote em tempo de design e na ordem especificada no pacote. (A única exceção a essa regra são as configurações de Variáveis do Pacote Pai. O utilitário só aplica essas configurações uma vez e posteriormente no processo.)  
  
3.  Em seguida, o utilitário aplica qualquer opção que você especificou na linha de comando.  
  
4.  O utilitário recarrega as configurações que foram especificadas no pacote em tempo de design e na ordem especificada no pacote. (Novamente, a exceção a essa regra são as configurações de Variáveis do Pacote Pai). O utilitário usa qualquer opção de linha de comando que foi especificada para recarregar as configurações. Portanto, valores diferentes podem ser recarregados a partir de locais distintos.  
  
5.  O utilitário aplica as configurações Variáveis do Pacote Pai.  
  
6.  O utilitário executa o pacote.  
  
 O modo como o utilitário **dtexec** aplica as configurações afeta as seguintes opções da linha de comando:  
  
-   Você pode usar a opção **/Connection** ou **/Set** na execução para carregar as configurações do pacote por meio de um local diferente do especificado no design.  
  
-   Você pode usar a opção **/ConfigFile** para carregar as configurações adicionais não especificadas no design.  
  
 Porém, essas opções de linha de comando têm algumas restrições:  
  
-   Não é possível usar a opção **/Set** ou **/Connection** para substituir os valores únicos que também são definidos por uma configuração.  
  
-   Não é possível usar a opção **/ConfigFile** para carregar as configurações que substituem as configurações especificadas no design.  
  
 Para obter mais informações sobre essas opções e sobre como o comportamento delas difere entre o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] e versões anteriores, consulte [Alterações de comportamento dos recursos do Integration Services no SQL Server 2016](../Topic/Behavior%20Changes%20to%20Integration%20Services%20Features%20in%20SQL%20Server%202016.md).  
  
## Tipos de configuração de pacotes  
 A tabela a seguir descreve os tipos de configuração de pacotes.  
  
|Tipo|Description|  
|----------|-----------------|  
|Arquivo de configuração XML|Um arquivo XML contém as configurações. O arquivo XML pode incluir várias configurações.|  
|Variável de ambiente|Uma variável de ambiente contém a configuração.|  
|Entrada de Registro|Uma entrada de Registro contém a configuração.|  
|Variável de pacote pai|Uma variável no pacote contém a configuração. Normalmente, esse tipo de configuração é usado para atualizar as propriedades em pacotes filho.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table|Uma tabela em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a configuração. A tabela pode incluir várias configurações.|  
  
### Arquivos de configuração XML  
 Se você selecionar o tipo de configuração **arquivo de configuração XML** , poderá criar um novo arquivo de configuração, reutilizar um arquivo existente e adicionar configurações novas ou reutilizar um arquivo existente, mas substituir o conteúdo do arquivo.  
  
 Um arquivo de configuração XML inclui duas seções:  
  
-   Um título que contém informações sobre o arquivo de configuração. Esse elemento inclui atributos tais como quando o arquivo foi criado e o nome da pessoa que gerou o arquivo.  
  
-   Elementos de configuração que contêm informações sobre cada configuração. Esse elemento inclui atributos como o caminho da propriedade e o valor configurado de uma propriedade.  
  
 O código XML a seguir mostra a sintaxe de um arquivo de configuração XML. Esse exemplo mostra uma configuração para a propriedade Value de uma variável de inteiro chamada `MyVar`.  
  
```  
<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
### Entrada de Registro  
 Se você desejar usar uma entrada de Registro para armazenar a configuração, poderá usar uma chave existente ou criar uma nova chave em HKEY_CURRENT_USER. A chave do Registro que você usa deve ter um valor denominado **Value**. O valor pode ser um DWORD ou uma cadeia de caracteres.  
  
 Se você selecionar o tipo de configuração **Entrada de Registro** , digitará o nome da chave do Registro na caixa de entrada de Registro. O formato é \<chave do Registro>. Se você quiser usar uma chave do Registro que não está na raiz de HKEY_CURRENT_USER, use o formato \<registry key\registry key\\...> para identificar a chave. Por exemplo, para usar a chave MyPackage localizada em SSISPackages, digite **SSISPackages\MyPackage**.  
  
### SQL Server  
 Se você selecionar o tipo de configuração **SQL Server** , especifique a conexão para o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que deseja armazenar as configurações. Você pode salvar as configurações em uma tabela existente ou criar uma tabela no banco de dados especificado.  
  
 A instrução SQL a seguir mostra a instrução padrão CREATE TABLE fornecida pelo Assistente de Configuração de Pacotes.  
  
```  
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 O nome fornecido para a configuração é o valor armazenado na coluna **ConfigurationFilter** .  
  
## Configurações diretas e indiretas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece configurações diretas e indiretas. Se você especificar as configurações diretamente, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um vínculo direto entre o item de configuração e a propriedade de objeto do pacote. As configurações diretas são a melhor escolha quando o local da origem não é alterado. Por exemplo, se você tiver certeza de que todas as implantações no pacote usam o mesmo caminho de arquivo, poderá especificar um arquivo de configuração XML.  
  
 As configurações indiretas usam variáveis de ambiente. Em vez de especificar os parâmetros de configuração diretamente, a configuração aponta para uma variável de ambiente que, por sua vez, contém o valor da configuração. O uso de configurações indiretas é a escolha mais adequada quando o local da configuração pode ser alterado em cada implantação de um pacote.  
  
## Tarefas relacionadas  
 [Criar configurações de pacote](../../integration-services/packages/create-package-configurations.md)  
  
## Conteúdo relacionado  
  
-   Artigo técnico de [Noções básicas sobre configurações de pacotes do Integration Services](http://go.microsoft.com/fwlink/?LinkId=165643), em msdn.microsoft.com  
  
-   Entrada de blog, [Criando pacotes em código – Configurações de Pacote](http://go.microsoft.com/fwlink/?LinkId=217663), em www.sqlis.com.  
  
-   Entrada de blog, [Exemplo de API – Adicione programaticamente um arquivo de configuração a um pacote](http://go.microsoft.com/fwlink/?LinkId=217664), em blogs.msdn.com.  
  
  
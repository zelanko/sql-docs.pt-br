---
title: Mostrar relações muitos para muitos em Hierarquias Derivadas
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8b2a9c43-40e0-48f7-a6a9-325beb9f27da
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c8f0a7536605af05457de13ebcd2011083386010
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811386"
---
# <a name="show-many-to-many-relationships-in-derived-hierarchies-master-data-services"></a>Mostrar relações muitos para muitos em Hierarquias Derivadas (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  As DHs (Hierarquias Derivadas) exibem relações um para muitos e, agora, também podem mostrar relações muitos para muitos.  
  
## <a name="many-to-many-m2m-relationships"></a>Relações M2M (muitos-para-muitos)  
 Uma relação M2M entre duas entidades pode ser modelada com o uso de uma terceira entidade que forneça um mapeamento entre elas:  
  
 ![mds_hierarchies_manytomany](../master-data-services/media/mds-hierarchies-manytomany.png "mds_hierarchies_manytomany")  
  
 No exemplo acima, há uma relação M2M entre as entidades **Employee** e **TrainingClass** , fornecidas pela entidade de mapeamento **ClassRegistration**. Um funcionário pode ser registrado como um aluno em várias classes, e cada classe pode conter vários alunos.  
  
 Anteriormente, as Hierarquias Derivadas não podiam modelar relações M2M. A partir do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], você pode criar uma Hierarquia Derivada que exiba, por exemplo, alunos por classe, ou inverta a relação e mostre classes agrupadas por alunos.  
  
 Em primeiro lugar, vá para a página de gerenciamento Hierarquia Derivada e crie uma nova Hierarquia Derivada:  
  
 ![mds_hierarchies_add_derived_hierarchy](../master-data-services/media/mds-hierarchies-add-derived-hierarchy.png "mds_hierarchies_add_derived_hierarchy")  
  
 Em seguida, adicione níveis à nova Hierarquia Derivada, começando de baixo para cima. Neste exemplo, queremos mostrar alunos (funcionários) agrupados por classe. A entidade **Employee** é, portanto, o nível folha da hierarquia, e é adicionado primeiro:  
  
 ![mds_hierarchies_edit_derived_hierarchy_one](../master-data-services/media/mds-hierarchies-edit-derived-hierarchy-one.PNG "mds_hierarchies_edit_derived_hierarchy_one")  
  
 Na captura de tela acima, observe que a entidade **Employee** aparece sob **Níveis Atuais** no meio como o único nível. A Hierarquia Derivada **Visualização** à direita simplesmente mostra uma lista de todos os membros da entidade **Employee** . A seção **Níveis Disponíveis** à esquerda mostra quais níveis podem ser adicionados no nível superior atual (**Funcionário**). A maioria deles são DBAs (atributos baseados em domínio) na entidade **Funcionário** , incluindo o DBA **Departamento** .  
  
 A partir do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], há um novo tipo de nível que modela as relações M2M, por exemplo: **Classe (mapeado por meio de ClassRegistration.Student)**. O nome do nível é mais detalhado do que os outros de modo a refletir as informações extras necessárias para descrever inequivocamente a relação de mapeamento. Arraste e solte esse nível no nível **Employee** na seção **Níveis Atuais** :  
  
 ![mds_hierarchies_edit_derived_hierarchy_two](../master-data-services/media/mds-hierarchies-edit-derived-hierarchy-two.PNG "mds_hierarchies_edit_derived_hierarchy_two")  
  
 Agora a visualização mostra os funcionários agrupados por classes de treinamento para as quais eles foram registrados. Como essa é uma relação M2M, cada membro filho pode ter vários pais. No exemplo acima, o funcionário **6 {Hillman, Reinout N}** foi registrado como um aluno em duas classes, **1 {Master Data Services 101}** e **4 {Career-Limiting Moves}**.  
  
 Essa relação de mapeamento também pode ser exibida de forma invertida, agrupando classes por aluno:  
  
 ![mds_hierarchies_available_entities_and_hierarchies](../master-data-services/media/mds-hierarchies-available-entities-and-hierarchies.PNG "mds_hierarchies_available_entities_and_hierarchies")  
  
 Novamente, vemos como um filho pode aparecer em mais de um pai: classe de treinamento **1 {Master Data Services 101}** aparece em **6 {Hillman, Reinout N}** e **40 {Ford, Jeffrey L}**.  
  
 Os membros da entidade de mapeamento **ClassRegistration** não aparecem em qualquer lugar na Hierarquia Derivada. Eles são usados simplesmente para definir as relações entre os membros pai e filho na hierarquia.  
  
 Você pode editar a relação M2M modificando os membros da entidade de mapeamento, executando uma das ações a seguir. A relação M2M é somente leitura na página **Gerenciador de Hierarquias Derivadas** .  
  
-   Modifique os membros da entidade de mapeamento na página **Gerenciador de Entidades** usando o suplemento Master Data Services para Excel ou usando os dados de preparo.  
  
-   Arraste e solte os nós filho entre pais na página **Gerenciador de Hierarquias Derivadas**.  
  
     Esse método modifica membros existentes quando possível e adiciona novos membros quando necessário. Membros existentes não são excluídos.  
  
     Por exemplo, com a entidade de mapeamento ClassRegistration, ao mover um aluno para o nó não utilizado, o valor do atributo da classe do membro da entidade de mapeamento correspondente é alterado para nulo, e o membro não é excluído. De modo inverso, ao mover um aluno do nó não utilizado para alguma classe, se existir um membro de mapeamento correspondente ao aluno onde a classe seja nula, esse membro será modificado alterando a classe de nulo para o novo pai. Se esse tipo de membro não for encontrado, um será adicionado.  
  
     Esse processo evita a exclusão do membro para impedir exclusão indesejada de dados de outro usuário, por exemplo, se a entidade de mapeamento contiver outros atributos além dos dois que definem a relação pai e filho. Os usuários devem fazer exclusões de modo explícito diretamente na entidade de mapeamento.  
  
 O novo nível M2M pode aparecer em qualquer lugar em uma Hierarquia Derivada em que um nível DBA (atributo baseado em domínio) é permitido. Um nível M2M pode estar no topo, como nos exemplos acima. Ele pode estar acima e/ou abaixo de um nível DBA, incluindo níveis recursivos. Ele pode estar abaixo de um nível Cap da Hierarquia Explícita (preterido). Várias relações M2M podem ser encadeadas na mesma Hierarquia Derivada.  
  
 Os níveis M2M podem estar ocultos, assim como outros níveis da Hierarquia Derivada.  
   
### <a name="m2m-relationship-in-sample-model"></a><a name="M2MSample"></a>Relação M2M no modelo de exemplo  
Para obter uma demonstração de uma relação M2M, exiba a hierarquia derivada Clima da Região no modelo de exemplo Cliente incluído no [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)].   
  
Como mostra a imagem a seguir, o nome do nível que modela essa relação é ![mds_Number1](../master-data-services/media/mds-number1.png)**Climate (mapeado por meio de RegionClimate.Region)**. O ![mds_Number2](../master-data-services/media/mds-number2.png)**Preview** mostra regiões agrupadas pelos tipos de climas aos quais elas estão associadas. Essa é uma relação M2M porque há regiões (membros filho) associadas a vários climas (pais). Por exemplo, ![mds_Number3](../master-data-services/media/mds-number3.png)**APCR {Asia Pacific}** está associado a ![mds_Number4](../master-data-services/media/mds-number4.png)**A {Tropical}** e ![mds_Number5](../master-data-services/media/mds-number5.png)**B {Dry}**.  
  
![mds_M2MRelationship_Example_CustomerModel](../master-data-services/media/mds-m2mrelationship-example-customermodel.png)  
  
Para obter instruções sobre como implantar o modelo de exemplo Cliente e outros modelos de exemplo incluídos no [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Implantando dados e modelos de exemplo](~/master-data-services/sql-server-samples-model-deployment-packages-mds.md).   
  
## <a name="one-many-relationship"></a>Relação um para muitos  
 Um membro de uma HD pode ser o pai de vários membros filho, mas, em geral, ele não pode ter mais de um pai (para ver as exceções, consulte [Segurança do membro](#bkmk_member_security)). Por exemplo, suponha que há duas entidades: Employee e Department, em que cada funcionário pertence a um único departamento. Essa relação é modelada adicionando à entidade Employee um DBA (atributo baseado em domínio) que faz referência à entidade Department:  
  
 ![mds_hierarchies_onetomany](../master-data-services/media/mds-hierarchies-onetomany.png "mds_hierarchies_onetomany")  
  
 Essa é uma relação um para muitos porque cada funcionário pertence a apenas um departamento, mas cada departamento pode ter vários funcionários. Uma Hierarquia Derivada pode ser criada exibindo funcionários por departamento:  
  
 ![mds_hierarchies_dh_screenshot](../master-data-services/media/mds-hierarchies-dh-screenshot.png "mds_hierarchies_dh_screenshot")  
  
##  <a name="member-security"></a><a name="bkmk_member_security"></a> Segurança do membro  
 Uma hierarquia que permite a duplicação do membro (permite que um membro tenha mais de um pai) não pode ser usada para atribuir permissões de segurança do membro. Por exemplo:  
  
-   Uma RDH (Hierarquia Derivada Recursiva) que não ancora recursões nulas (cada membro no nível recursivo aparece sob ROOT e seu pai recursivo).  
  
-   Uma Hierarquia Derivada Recursiva com um nível acima do nível recursivo (cada membro do nível recursivo aparece sob seu pai não recursivo e seu pai recursivo).  
  
-   Uma Hierarquia Derivada com um nível M2M (um filho pode ser mapeado para muitos pais).  
  
## <a name="collections"></a>Coleções  
 As Coleções e Hierarquias Explícitas foram preteridas. O procedimento armazenado de conversão (udpConvertCollectionAndConsolidatedMembersToLeaf) converte membros da coleção em membros folha e cria Hierarquias Derivadas muitos para muitos para capturar informações de associação de coleção.  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquias derivadas &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  

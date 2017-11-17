---
title: CRIAR o ASSEMBLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 8/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASSEMBLY
- CREATE ASSEMBLY
- CREATE_ASSEMBLY_TSQL
- ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], validating
- validating assemblies
- CREATE ASSEMBLY statement
- assemblies [CLR integration], creating
ms.assetid: d8d1d245-c2c3-4325-be52-4fc1122c2079
caps.latest.revision: 94
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 845175405b8acc810044c0acc1f54060b81280d4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-assembly-transact-sql"></a>CREATE ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um módulo de aplicativo gerenciado que contém metadados de classe e código gerenciado como um objeto em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao fazer referência a esse módulo, funções CLR (Common Language Runtime), procedimentos armazenados, gatilhos, agregações definidas pelo usuário e tipos definidos pelo usuário podem ser criados no banco de dados.  
  
>  [!WARNING]
>  O CLR usa o CAS (Segurança de Acesso do Código) no .NET Framework, para o qual não há mais suporte como um limite de segurança. Um assembly CLR criado com o `PERMISSION_SET = SAFE` pode conseguir acessar recursos externos do sistema, chamar um código não gerenciado e adquirir privilégios sysadmin. A partir do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], uma opção `sp_configure` chamada `clr strict security` é introduzida, a fim de aumentar a segurança de assemblies CLR. A `clr strict security` está habilitada por padrão e trata assemblies `SAFE` e `EXTERNAL_ACCESS` como se eles fossem marcados como `UNSAFE`. A opção `clr strict security` pode ser desabilitada para compatibilidade com versões anteriores, mas isso não é recomendado. A Microsoft recomenda que todos os assemblies sejam assinados por um certificado ou uma chave assimétrica com um logon correspondente que recebeu a permissão `UNSAFE ASSEMBLY` no banco de dados mestre. Para obter mais informações, consulte [Segurança estrita do CLR](../../database-engine/configure-windows/clr-strict-security.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE ASSEMBLY assembly_name  
[ AUTHORIZATION owner_name ]  
FROM { <client_assembly_specifier> | <assembly_bits> [ ,...n ] }  
[ WITH PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE } ]  
[ ; ]  
<client_assembly_specifier> :: =  
        '[\\computer_name\]share_name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome_do_assembly*  
 É o nome do assembly. O nome deve ser exclusivo no banco de dados e uma opção válida [identificador](../../relational-databases/databases/database-identifiers.md).  
  
 AUTORIZAÇÃO *owner_name*  
 Especifica o nome de um usuário ou função como proprietário do assembly. *owner_name* deve ser o nome de uma função da qual o usuário atual é um membro ou o usuário atual deve ter a permissão IMPERSONATE no *owner_name*. Se não estiver especificada, a propriedade será dada ao usuário atual.  
  
 \<client_assembly_specifier >  
Especifica o caminho local ou o local da rede onde o assembly que está sendo carregado está localizado e também o nome do arquivo de manifesto que corresponde ao assembly.  \<client_assembly_specifier > pode ser expresso como uma cadeia de caracteres fixa ou uma expressão que avalia para uma cadeia de caracteres fixa, com variáveis. CREATE ASSEMBLY não dá suporte ao carregamento de assemblies de vários módulos. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também procura assemblies dependentes desse assembly no mesmo lugar e os carrega com o mesmo proprietário do assembly do nível raiz. Se esses assemblies dependentes não forem encontrados e eles já não estiverem carregados no banco de dados atual, CREATE ASSEMBLY falhará. Se os assemblies dependentes já estiverem carregados no banco de dados atual, o proprietário deles deve ser o mesmo proprietário do assembly recém-criado.
  
 \<client_assembly_specifier > não pode ser especificado se o usuário conectado que está sendo representado.  
  
 \<assembly_bits >  
 É a lista de valores binários que compõe o assembly e seus assemblies dependentes. O primeiro valor na lista é considerado o assembly do nível raiz. Os valores correspondentes aos assemblies dependentes podem ser fornecidos em qualquer ordem. Qualquer valor que não corresponda a dependências do assembly raiz será ignorado.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 *varbinary_literal*  
 É um **varbinary** literal.  
  
 *varbinary_expression*  
 É uma expressão do tipo **varbinary**.  
  
 PERMISSION_SET { **SEGURO** | EXTERNAL_ACCESS | UNSAFE}  
 >  [!IMPORTANT]  
 >  O `PERMISSION_SET` opção é afetada pelo `clr strict security` opção, descrita no aviso de abertura. Quando `clr strict security` é habilitada, todos os assemblies são tratados como `UNSAFE`.
 
 Especifica um conjunto de permissões de acesso de código que são concedidas ao assembly quando ele é acessado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se não especificado, SAFE será aplicado por padrão.  
  
 É recomendável o uso de SAFE. SAFE é o conjunto de permissões mais restritivo. O código executado por um assembly com as permissões SAFE não pode acessar recursos externos do sistema, como arquivos, a rede, variáveis de ambiente ou o Registro.  
  
 EXTERNAL_ACCESS permite que os assemblies acessem certos recursos externos do sistema, como arquivos, redes, variáveis de ambiente e o Registro.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 UNSAFE concede aos assemblies acesso irrestrito aos recursos, internos ou externos, de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O código executado a partir de um assembly UNSAFE pode chamar um código não gerenciado.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
> [!IMPORTANT]  
>  SAFE é a configuração de permissão recomendada para assemblies que executam tarefas de computação e de gerenciamento de dados sem acessar recursos externos de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
>   
>  É recomendável o uso de EXTERNAL_ACCESS para assembly que acessam recursos fora de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Assemblies EXTERNAL_ACCESS possuem proteções de confiabilidade e escalabilidade dos assemblies SAFE, mas com uma perspectiva de segurança similar a de assemblies UNSAFE. Isso porque o código de assemblies EXTERNAL_ACCESS é executado, por padrão, em uma conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e acessa recursos externos por essa conta, exceto se o código representar explicitamente o chamador. Portanto, a permissão para criar assemblies EXTERNAL_ACCESS ser concedida apenas para logons confiáveis para executar o código pela conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre representação, consulte [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md).  
>   
>  A especificação de UNSAFE proporciona ao código do assembly liberdade total para executar operações no espaço de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o que pode comprometer a robustez do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Assemblies UNSAFE também podem potencialmente subverter o sistema de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do CLR. Permissões UNSAFE devem ser concedidas exclusivamente para assemblies altamente confiáveis. Somente membros do **sysadmin** função de servidor fixa pode criar e alterar assemblies UNSAFE.  
  
 Para obter mais informações sobre conjuntos de permissões de assembly, consulte [projetar Assemblies](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="remarks"></a>Comentários  
 CREATE ASSEMBLY carrega um assembly previamente compilado como um arquivo .dll a partir do código gerenciado para uso dentro de uma instância do SQL Server.  
 
Quando habilitada, a opção `PERMISSION_SET` nas instruções `CREATE ASSEMBLY` e `ALTER ASSEMBLY` é ignorada em tempo de execução, mas as opções `PERMISSION_SET` são preservadas nos metadados. Ignorar a opção minimiza a interrupção de instruções de código existentes.
 
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite o registro de versões diferentes de um assembly com nome, cultura e chave pública iguais.  
  
Ao tentar acessar o assembly especificado em \<client_assembly_specifier >, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] representa o contexto de segurança do logon atual do Windows. Se \<client_assembly_specifier > especifica um local de rede (caminho UNC), a representação do logon atual não é repassada ao local de rede devido a limitações de delegação. Nesse caso, o acesso é feito usando o contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [credenciais &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md).
  
 Além do assembly raiz especificado por *nome_do_assembly*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta carregar todos os assemblies que são referenciados pelo assembly raiz que está sendo carregado. Se já houver um assembly referenciado carregado no banco de dados devido a uma instrução CREATE ASSEMBLY anterior, esse assembly não será carregado, mas estará disponível para o assembly raiz. Se não houver um assembly dependente carregado, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não conseguir localizar seu arquivo de manifesto no diretório de origem, CREATE ASSEMBLY retornará um erro.  
  
 Se algum dos assemblies dependentes referenciados pelo assembly raiz ainda não foi carregado no banco de dados mas foi carregado implicitamente com o assembly raiz, ambos terão o mesmo conjunto de permissões que o assembly do nível raiz. Se for necessário criar os assemblies dependentes usando um conjunto de permissões diferente daquele usado pelo assembly de nível raiz, ambos terão que ser carregados explicitamente antes do assembly do nível raiz com o conjunto de permissões apropriado.  
  
## <a name="assembly-validation"></a>Validação de assembly  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa verificações nos binários de assembly carregados pela instrução CREATE ASSEMBLY para garantir o seguinte:  
  
-   O binário de assembly está bem formado com metadados e segmentos de código válidos, e os segmentos de código têm instruções do Microsoft Intermediate Language (MSIL) válidas.  
  
-   O conjunto de assemblies de sistema a que ele faz referência é um dos seguintes assemblies suportados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: Microsoft.Visualbasic.dll, Mscorlib.dll, System.Data.dll, System.dll, System.Xml.dll, Microsoft.Visualc.dll, Custommarshallers.dll, System.Security.dll, System.Web.Services.dll, System.Data.SqlXml.dll, System.Core.dll e System.Xml.Linq.dll. Outros assemblies de sistema podem ser referenciados, mas eles devem ser registrados explicitamente no banco de dados.  
  
-   Para assemblies criados usando os conjuntos de permissões SAFE ou EXTERNAL ACCESS:  
  
    -   O código do assembly deve ser do tipo seguro. A segurança do tipo é estabelecida pela execução do verificador do CLR no assembly.  
  
    -   O assembly não deve conter membros de dados estáticos em suas classes a menos que eles sejam marcados como somente leitura.  
  
    -   As classes do assembly não podem conter métodos finalizadores.  
  
    -   As classes ou os métodos do assembly devem ser anotados somente com os atributos de código permitidos. Para obter mais informações, consulte [atributos personalizados para rotinas de CLR](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
 Além das verificações anteriores realizadas durante a execução de CREATE ASSEMBLY, existem duas verificações adicionais que são realizadas no tempo de execução do código no assembly:  
  
-   Chamada de determinadas [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] APIs que requerem uma permissão de acesso de código específica pode falhar se o conjunto de permissões do assembly não inclui essa permissão.  
  
-   Para assemblies SAFE e EXTERNAL_ACCESS, qualquer tentativa de chamar APIs [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que são anotadas com certos HostProtectionAttributes falhará.  
  
 Para obter mais informações, consulte [projetar Assemblies](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE ASSEMBLY.  
  
 Se PERMISSION_SET = EXTERNAL_ACCESS for especificado, requer**EXTERNAL ACCESS ASSEMBLY** permissão no servidor. Se PERMISSION_SET = UNSAFE for especificado, requer **UNSAFE ASSEMBLY** permissão no servidor.  
  
 O usuário deve ser o proprietário de todos os assemblies referenciados pelo assembly que será carregado se já houver assemblies no banco de dados. Para carregar um assembly usando um caminho de arquivo, o usuário atual deve ser um logon autenticado do Windows ou um membro do **sysadmin** função de servidor fixa. O logon do Windows do usuário que executa CREATE ASSEMBLY deve ter permissão de leitura no compartilhamento e para os arquivos que estão sendo carregados na instrução.  

### <a name="permissions-with-clr-strict-security"></a>Permissões de segurança estrita do CLR    
As seguintes permissões necessárias para criar um assembly CLR quando o `CLR strict security` está habilitado:

- O usuário deve ter a permissão `CREATE ASSEMBLY`  
- Além disso, uma das seguintes condições também deve ser verdadeira:  
  - O assembly é assinado com um certificado ou uma chave assimétrica que tem um logon correspondente à permissão `UNSAFE ASSEMBLY` no servidor. A assinatura do assembly é recomendada.  
  - O banco de dados tem a propriedade `TRUSTWORTHY` definida como `ON` e o banco de dados pertence a um logon que tem a permissão `UNSAFE ASSEMBLY` no servidor. Essa opção não é recomendada.  
  
 Para obter mais informações sobre conjuntos de permissões de assembly, consulte [projetar Assemblies](../../relational-databases/clr-integration/assemblies-designing.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="example-a-creating-an-assembly-from-a-dll"></a>Exemplo a: Criando um assembly a partir de uma dll  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O exemplo a seguir supõe que há exemplos do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] instalados no local padrão do computador local e que o aplicativo de exemplo HelloWorld.csproj esteja compilado. Para obter mais informações, consulte [exemplo Hello World](http://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7).  
  
```  
CREATE ASSEMBLY HelloWorld   
FROM <system_drive>:\Program Files\Microsoft SQL Server\100\Samples\HelloWorld\CS\HelloWorld\bin\debug\HelloWorld.dll  
WITH PERMISSION_SET = SAFE;  
```  
  
### <a name="example-b-creating-an-assembly-from-assembly-bits"></a>Exemplo b: Criando um assembly de bits do assembly  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Substitua os bits de exemplo (que não são válidos ou concluída) com os bits do assembly.  
  
```  
CREATE ASSEMBLY HelloWorld  
    FROM 0x4D5A900000000000  
WITH PERMISSION_SET = SAFE;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [DROP ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [Criar agregação &#40; Transact-SQL &#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Cenários de uso e exemplos de Common Language Runtime &#40; CLR &#41; Integração](http://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
  
  


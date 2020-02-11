---
title: Referência de erro ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da9d7d2374f8e3410598bfdfbd97e59eb505b255
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926241"
---
# <a name="ado-errors"></a>Erros ADO
A constante **ErrorValueEnum** descreve os valores de erro do ADO. Para obter uma lista completa dessas constantes enumeradas, incluindo valores, consulte o [Apêndice B: erros do ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md). Esta seção examinará alguns dos erros mais interessantes e explicará algumas situações específicas que podem gerar essas informações ou soluções para corrigir o problema. A constante **ErrorValueEnum** e o número decimal positivo curto são listados.

|Número|Constante ErrorValueEnum|Descrição/possíveis causas|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|O provedor não pôde executar a operação solicitada.|
|**3001**|**adErrInvalidArgument**|Os argumentos são do tipo incorreto, estão fora do intervalo aceitável ou estão em conflito uns com os outros. Esse erro geralmente é causado por um erro tipográfico em uma instrução SQL SELECT. Por exemplo, um nome de campo ou nome de tabela digitado incorretamente pode gerar esse erro. Esse erro também pode ocorrer quando um campo ou tabela nomeada em uma instrução SELECT não existe no repositório de dados.|
|**3002**|**adErrOpeningFile**|Não foi possível abrir o arquivo. Um nome de arquivo digitado incorretamente foi especificado ou um arquivo foi movido, renomeado ou excluído. Em uma rede, a unidade pode estar temporariamente indisponível ou o tráfego de rede pode estar impedindo uma conexão.|
|**3003**|**adErrReadFile**|Não foi possível ler o arquivo. O nome do arquivo está especificado incorretamente, o arquivo pode ter sido movido ou excluído, ou o arquivo pode ter se tornado corrompido.|
|**3004**|**adErrWriteFile**|Falha ao gravar no arquivo. Você pode ter fechado um arquivo e, em seguida, tentado gravar nele, ou o arquivo pode estar corrompido. Se o arquivo estiver localizado em uma unidade de rede, as condições de rede transitórias podem impedir a gravação em uma unidade de rede.|
|**3021**|**adErrNoCurrentRecord**|**BOF** ou **EOF** é true ou o registro atual foi excluído. A operação solicitada requer um registro atual.<br /><br /> Foi feita uma tentativa de atualizar registros usando **Localizar** ou **buscar** para mover o ponteiro de registro para o registro desejado. Se o registro não for encontrado, **EOF** será true. Esse erro também pode ocorrer após um **AddNew** ou **delete** com falha porque não há registro atual quando esses métodos falham.|
|**3219**|**adErrIllegalOperation**|A operação não é permitida neste contexto.|
|**3220**|**adErrCantChangeProvider**|O provedor fornecido é diferente do que já está em uso.|
|**3246**|**adErrInTransaction**|O objeto de **conexão** não pode ser fechado explicitamente durante uma transação. Um **conjunto de registros** ou objeto de **conexão** que está atualmente participando de uma transação não pode ser fechado. Chame **RollbackTrans** ou **CommitTrans** antes de fechar o objeto.|
|**3251**|**adErrFeatureNotAvailable**|O objeto ou provedor não é capaz de executar a operação solicitada. Algumas operações dependem de uma versão de provedor específica.|
|**3265**|**adErrItemNotFound**|Não é possível encontrar o item na coleção correspondente ao nome ou ordinal solicitado. Um campo ou nome de tabela incorreto foi especificado.|
|**3367**|**adErrObjectInCollection**|O objeto já está na coleção. Não é possível acrescentar. Não é possível adicionar um objeto à mesma coleção duas vezes.|
|**3420**|**adErrObjectNotSet**|O objeto não é mais válido.|
|**3421**|**adErrDataConversion**|O aplicativo usa um valor do tipo incorreto para a operação atual. Você pode ter fornecido uma cadeia de caracteres para uma operação que espera um fluxo, por exemplo.|
|**3704**|**adErrObjectClosed**|A operação não é permitida quando o objeto é fechado. A **conexão** ou o **conjunto de registros** foi fechado. Por exemplo, alguma outra rotina pode ter fechado um objeto global. Você pode evitar esse erro verificando a propriedade de **estado** antes de tentar uma operação.|
|**3705**|**adErrObjectOpen**|A operação não é permitida quando o objeto está aberto. Não é possível abrir um objeto aberto. Os campos não podem ser anexados a um **conjunto de registros**aberto.|
|**3706**|**adErrProviderNotFound**|Provedor não encontrado. Ele pode não estar instalado corretamente.<br /><br /> O nome do provedor pode ser especificado incorretamente, o provedor especificado pode não estar instalado no computador em que o código está sendo executado ou a instalação pode ter sido corrompida.|
|**3707**|**adErrBoundToCommand**|A propriedade **ActiveConnection** de um objeto **Recordset** , que tem um objeto **Command** como sua origem, não pode ser alterada. O aplicativo tentou atribuir um novo objeto de **conexão** a um **conjunto de registros** que tem um objeto de **comando** como sua origem.|
|**3708**|**adErrInvalidParamInfo**|O objeto de **parâmetro** está definido incorretamente. Informações inconsistentes ou incompletas foram fornecidas.|
|**3709**|**adErrInvalidConnection**|A conexão não pode ser usada para executar esta operação. Ele está fechado ou é inválido neste contexto.|
|**3710**|**adErrNotReentrant**|A operação não pode ser executada durante o processamento do evento. Uma operação não pode ser executada em um manipulador de eventos que faz com que o evento seja acionado novamente. Por exemplo, os métodos de navegação não devem ser chamados de dentro de um manipulador de eventos **WillMove** .|
|**3711**|**adErrStillExecuting**|A operação não pode ser executada durante a execução assíncrona.|
|**3712**|**adErrOperationCancelled**|A operação foi cancelada pelo usuário. O aplicativo chamou o método **CancelUpdate** ou **CancelBatch** e a operação atual foi cancelada.|
|**3713**|**adErrStillConnecting**|Não é possível executar a operação durante a conexão assíncrona.|
|**3714**|**adErrInvalidTransaction**|A transação de coordenação é inválida ou não foi iniciada.|
|**3715**|**adErrNotExecuting**|Não é possível executar a operação enquanto não estiver em execução.|
|**3716**|**adErrUnsafeOperation**|As configurações de segurança neste computador proíbem o acesso a uma fonte de dados em outro domínio.|
|**3717**|**adWrnSecurityDialog**|Apenas para uso interno. Não use. (A entrada foi incluída para fins de integridade. Esse erro não deve aparecer no seu código.)|
|**3718**|**adWrnSecurityDialogHeader**|Apenas para uso interno. Não use. (Entrada incluída para fins de integridade. Esse erro não deve aparecer no seu código.)|
|**3719**|**adErrIntegrityViolation**|O valor dos dados está em conflito com as restrições de integridade do campo. Um novo valor para um **campo** poderia causar uma chave duplicada. Um valor que forma um lado de uma relação entre dois registros pode não ser atualizável.|
|**3720**|**adErrPermissionDenied**|Permissão insuficiente impede a gravação no campo. O usuário nomeado na cadeia de conexão não tem as permissões adequadas para gravar em um **campo**.|
|**3721**|**adErrDataOverflow**|O valor dos dados é muito grande para ser representado pelo tipo de dados Field. Um valor numérico muito grande para o campo pretendido foi atribuído. Por exemplo, um valor inteiro longo foi atribuído a um campo inteiro curto.|
|**3722**|**adErrSchemaViolation**|O valor dos dados está em conflito com o tipo de dados ou as restrições do campo. O armazenamento de dados tem restrições de validação que diferem do valor do **campo** .|
|**3723**|**adErrSignMismatch**|Falha na conversão porque o valor de dados estava assinado e o tipo de dados de campo usado pelo provedor não estava assinado.|
|**3724**|**adErrCantConvertvalue**|O valor de dados não pode ser convertido por razões diferentes de incompatibilidade de sinal ou estouro de dados. Por exemplo, a conversão teria dados truncados.|
|**3725**|**adErrCantCreate**|O valor de dados não pode ser definido ou recuperado porque o tipo de dados do campo era desconhecido ou o provedor tinha recursos insuficientes para executar a operação.|
|**3726**|**adErrColumnNotOnThisRow**|O registro não contém este campo. Um nome de campo incorreto foi especificado ou um campo que não está na coleção de **campos** do registro atual foi referenciado.|
|**3727**|**adErrURLDoesNotExist**|A URL de origem ou o pai da URL de destino não existe. Há um erro tipográfico na URL de origem ou de destino. Você pode ter `https://mysite/photo/myphoto.jpg` quando deve realmente ter `https://mysite/photos/myphoto.jpg` em vez disso. O erro tipográfico na URL pai (neste caso, *foto* em vez de *fotos*) causou o erro.|
|**3728**|**adErrTreePermissionDenied**|As permissões são insuficientes para acessar árvore ou subárvore. O usuário nomeado na cadeia de conexão não tem as permissões apropriadas.|
|**3729**|**adErrInvalidURL**|A URL contém caracteres inválidos. Verifique se a URL foi digitada corretamente. A URL segue o esquema registrado para o provedor atual (por exemplo, o provedor de publicação da Internet é registrado para http).|
|**3730**|**adErrResourceLocked**|O objeto representado pela URL especificada está bloqueado por um ou mais processos. Aguarde até que o processo seja concluído e tente a operação novamente. O objeto que você está tentando acessar foi bloqueado por outro usuário ou por outro processo em seu aplicativo. Isso provavelmente ocorrerá em um ambiente de vários usuários.|
|**3731**|**adErrResourceExists**|Não é possível executar a operação de cópia. O objeto nomeado pela URL de destino já existe. Especifique **adCopyOverwrite** para substituir o objeto. Se você não especificar **adCopyOverwrite** ao copiar os arquivos em um diretório, a cópia falhará quando você tentar copiar um item que já existe no local de destino.|
|**3732**|**adErrCannotComplete**|O servidor não pode concluir a operação. Isso pode ocorrer porque o servidor está ocupado com outras operações ou pode estar com poucos recursos.|
|**3733**|**adErrVolumeNotFound**|O provedor não pode localizar o dispositivo de armazenamento indicado pela URL. Verifique se a URL foi digitada corretamente. A URL do dispositivo de armazenamento pode estar incorreta, mas esse erro pode ocorrer por outros motivos. O dispositivo pode estar offline ou um grande volume de tráfego de rede pode impedir que a conexão seja feita.|
|**3734**|**adErrOutOfSpace**|Não é possível executar a operação. O provedor não pode obter espaço de armazenamento suficiente. Pode não haver RAM suficiente ou espaço de disco rígido para arquivos temporários no servidor.|
|**3735**|**adErrResourceOutOfScope**|A URL de origem ou de destino está fora do escopo do registro atual.|
|**3736**|**adErrUnavailable**|A operação não foi concluída e o status não está disponível. O campo pode estar indisponível ou a operação não foi tentada. Outro usuário pode ter alterado ou excluído o campo que você está tentando acessar.|
|**3737**|**adErrURLNamedRowDoesNotExist**|O registro nomeado por esta URL não existe. Ao tentar abrir um arquivo usando um objeto de **registro** , o nome do arquivo ou o caminho para o arquivo foi digitado incorretamente.|
|**3738**|**adErrDelResOutOfScope**|A URL do objeto a ser excluído está fora do escopo do registro atual.|
|**3747**|**adErrCatalogNotSet**|A operação requer um **ParentCatalog**válido.|
|**3748**|**adErrCantChangeConnection**|A conexão foi negada. A nova conexão solicitada tem características diferentes daquelas que já estão em uso.|
|**3749**|**adErrFieldsUpdateFailed**|Falha na atualização dos campos. Para obter mais informações, examine a propriedade **status** de objetos de campo individuais. Esse erro pode ocorrer em duas situações: ao alterar o valor de um objeto de **campo** no processo de alteração ou adição de um registro ao banco de dados; e ao alterar as propriedades do próprio objeto **Field** .<br /><br /> A atualização do **registro** ou do **conjunto de registros** falhou devido a um problema com um dos campos no registro atual. Enumere a coleção **Fields** e verifique a propriedade **status** de cada campo para determinar a causa do problema.|
|**3750**|**adErrDenyNotSupported**|O provedor não oferece suporte a restrições de compartilhamento. Foi feita uma tentativa de restringir o compartilhamento de arquivos e seu provedor não oferece suporte ao conceito.|
|**3751**|**adErrDenyTypeNotSupported**|O provedor não oferece suporte ao tipo solicitado de restrição de compartilhamento. Foi feita uma tentativa de estabelecer um tipo específico de restrição de compartilhamento de arquivos que não é suportado pelo seu provedor. Consulte a documentação do provedor para determinar quais restrições de compartilhamento de arquivos têm suporte.|

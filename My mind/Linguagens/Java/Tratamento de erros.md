------------------------------------------------
### Try-catch

try {
    // Código que pode lançar uma exceção
} catch (Tipo_Excecao variavel_erro) {
    // Código para tratar a exceção
} finally {
    // Código que será sempre executado
}

-------------------------
##### Exceções:

NullPointerException               = Quando se tem uma variável com valor null/vazio.
ArrayIndexOutOfBoundsException     = Quando se tenta acessar um elemento de um array utilizando um índice que não existe.
FileNotFoundException              = Quando se tentar abrir um arquivo que não existe no caminho especificado.
AlreadyBoundException              = Quando se tenta salvar um arquivo com um nome que já existe no diretório.
BadBinaryOpValueExpException       = Quando os argumentos de uma operação binária (ex: "maior que") são incompatíveis.
BadLocationException               = Quando se tenta acessar uma posição inválida em um documento de texto.
BadStringOperationException        = Quando se tenta aplicar uma operação de string em um valor que não é uma string.
CloneNotSupportedException         = Quando se chama o método clone() em um objeto cuja classe não implementa a interface.
DataFormatException                = Quando um formato de dados incorreto foi encontrado. Comum em (compressão/descompressão).
FontFormatException                = Quando se tenta criar uma fonte a partir de um arquivo, mas a fonte esta corrompida.
GeneralSecurityException           = Quando há falhas em criptografia ou verificação de assinaturas.
IllegalClassFormatException        = Quando se muda o formato bytecode de uma variavel que é inválido ou malformado.
IntrospectionException             = Ocorre se houver um erro durante o processo de introspecção de uma classe Java.
IOException                        = É uma exceção genérica para qualquer falha de Entrada/Saída.
JMException                        = Exceção genérica para qualquer problema que ocorra no sistema de (JMX).
KeySelectorException               = Ocorre quando há uma falha ao tentar encontrar a chave de API´s.
LambdaConversionException          = Se houver um problema ao converter uma expressão lambda para uma instância.
MimeTypeParseException             = Quando uma string que deveria representar um MIME Type (como "text/html") está malformada.
ParseException                     = Indica que ocorreu em converter o tipo de um objeto/variavel.
NamingException                    = Indica um erro genérico durante uma operação de busca ou nomeação em um diretório.
NotBoundException                  = Quando você tenta procurar um recurso por um nome, mas esse nome não está registrado.
PropertyVetoException              = Quando uma alteração em uma propriedade de um objeto é vetada (rejeitada).
ReflectiveOperationException       = Captura diversos tipos de exceções relacionadas à Reflexão (Reflection),
RefreshFailedException             = Quando uma tentativa de renovar ou atualizar credenciais de segurança falha.
RuntimeException                   = Erros em gerais.
SAXException                       = Ocorre durante a leitura do XML.
ScriptException                    = Indica que ocorreu um erro durante a execução de um script
SQLException                       = Indica que ocorreu um erro durante uma operação com um banco de dados.
StringConcatException              = Quando ocorre um erro durante o processo otimizado de concatenação de strings.




TimeoutException, 
TooManyListenersException,
TransformerException,
TransformException,
UnmodifiableClassException,
UnsupportedAudioFileException,
UnsupportedCallbackException,
UnsupportedFlavorException,
UnsupportedLookAndFeelException,






URIReferenceException, URISyntaxException, VMStartException, XAException, XMLParseException, XMLSignatureException, XMLStreamException, XPathException


һ��zeptoģ��ĵĴ
1.��https://github.com/madrobby/zepto����zepto��Ŀ
2.����Ŀ��build�Լ���Ҫ��zeptoģ��
You will need Node.js installed on your system.
$ npm install
$ npm run-script dist
# do a custom build
$ MODULES="zepto event data" npm run-script dist

ע�⣺MODULES ������windows�±���
�������������������������޸�zepto�ļ����µ�make�ļ��ĵ�42�У�
  modules = (env['MODULES'] || 'zepto event ajax form ie data touch fx fx_methods').split(' ')
��������Ҫ��ģ�鱣�棬Ȼ������npm run-script dist�Ϳ�

����zeptoʹ�õ�һЩע���
http://www.cnblogs.com/samwu/archive/2013/06/06/3121649.html
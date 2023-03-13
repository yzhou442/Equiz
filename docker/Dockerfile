FROM bitnami/moodle:4.0.5

RUN apt-get update && apt-get -y install git wget

# Additional question behaviours for STACK
RUN sed -i '/info\s"Trying\sto\sconnect\sto\sthe\sdatabase\sserver"/i git clone https://github.com/maths/moodle-qbehaviour_dfexplicitvaildate.git /bitnami/moodle/question/behaviour/dfexplicitvaildate' /opt/bitnami/scripts/libmoodle.sh
RUN sed -i '/info\s"Trying\sto\sconnect\sto\sthe\sdatabase\sserver"/i git clone https://github.com/maths/moodle-qbehaviour_dfcbmexplicitvaildate.git /bitnami/moodle/question/behaviour/dfcbmexplicitvaildate' /opt/bitnami/scripts/libmoodle.sh
RUN sed -i '/info\s"Trying\sto\sconnect\sto\sthe\sdatabase\sserver"/i git clone https://github.com/maths/moodle-qbehaviour_adaptivemultipart.git /bitnami/moodle/question/behaviour/adaptivemultipart' /opt/bitnami/scripts/libmoodle.sh
# STACK question type
RUN sed -i '/info\s"Trying\sto\sconnect\sto\sthe\sdatabase\sserver"/i git clone https://github.com/maths/moodle-qtype_stack.git /bitnami/moodle/question/type/stack' /opt/bitnami/scripts/libmoodle.sh
# CodeRunner question type
RUN sed -i '/info\s"Trying\sto\sconnect\sto\sthe\sdatabase\sserver"/i git clone  https://github.com/trampgeek/moodle-qtype_coderunner.git /bitnami/moodle/question/type/coderunner' /opt/bitnami/scripts/libmoodle.sh
# Additional question behaviours for codeRunner
RUN sed -i '/info\s"Trying\sto\sconnect\sto\sthe\sdatabase\sserver"/i git clone https://github.com/trampgeek/moodle-qbehaviour_adaptive_adapted_for_coderunner.git /bitnami/moodle/question/behaviour/adaptive_adapted_for_coderunner' /opt/bitnami/scripts/libmoodle.sh
# Install Maxima
RUN apt-get update && apt-get -y install maxima gnuplot gcc
# Install Collapsed Topics plugin
RUN apt-get update && apt-get -y install zip unzip
RUN sed -i '/info\s"Trying\sto\sconnect\sto\sthe\sdatabase\sserver"/i mkdir -p /bitnami/moodle/course/format/topcoll \&\& \
wget https://github.com/gjb2048/moodle-format_topcoll/archive/refs/tags/V400.1.2.zip -P /bitnami/moodle/course/format/topcoll \&\& \
unzip /bitnami/moodle/course/format/topcoll/V400.1.2.zip -d /bitnami/moodle/course/format/topcoll/ \&\& \
mv /bitnami/moodle/course/format/topcoll/moodle-format_topcoll-400.1.2/* /bitnami/moodle/course/format/topcoll/ \&\& \
rm -r /bitnami/moodle/course/format/topcoll/moodle-format_topcoll-400.1.2' /opt/bitnami/scripts/libmoodle.sh
# Install OU multiple response plugin
RUN sed -i '140 i mkdir -p /bitnami/moodle/question/type/oumultiresponse \&\& \
wget https://moodle.org/plugins/download.php/21651/qtype_oumultiresponse_moodle39_2020031600.zip -P /bitnami/moodle/question/type/oumultiresponse/ \&\& \
unzip /bitnami/moodle/question/type/oumultiresponse/qtype_oumultiresponse_moodle39_2020031600.zip -d /bitnami/moodle/question/type/oumultiresponse/ \&\& \
mv /bitnami/moodle/question/type/oumultiresponse/oumultiresponse/* /bitnami/moodle/question/type/oumultiresponse/ \&\& \
rm -r /bitnami/moodle/question/type/oumultiresponse/oumultiresponse' /opt/bitnami/scripts/libmoodle.sh
# Fix LTI issues
COPY commands.sh /
RUN chmod 777 commands.sh
RUN sed -i "29i     /commands.sh" /opt/bitnami/scripts/moodle/entrypoint.sh
#RUN sed -i '/info\s\"\*\*\sMoodle\ssetup\sfinished!\s\*\*\"/i sed -i "46 i \\$http_url = \\$scheme . '://' . getenv('MOODLE_HOST') . \\$_SERVER['REQUEST_URI'];" /bitnami/moodle/lib/ltiprovider/src/OAuth/OAuthRequest.php' /opt/bitnami/scripts/moodle/entrypoint.sh

# config php-fpm
RUN sed -i "440i pm = static" /opt/bitnami/php/etc/php-fpm.d/www.conf
RUN sed -i "441i pm.max_children = 1536" /opt/bitnami/php/etc/php-fpm.d/www.conf



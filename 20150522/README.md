# �f�[�^�x�[�X�ɂ��� 2015/05/22

## JOIN�i�����j

### ER�}

�uWWW SQL designer�v�𗘗p���āAER�}��`���Ă݂��B

![ER�}](ER.png)

### ����A�J�E���g�̒a����������
#### ���Ȍ����H

    SELECT a.ID, p.BIRTHDATE FROM ACCOUNT a, PROFILE p WHERE a.ID = 222183 AND p.ACCOUNT_ID = 222183;

0.003�b

#### ��������

    SELECT PROFILE.BIRTHDATE FROM ACCOUNT INNER JOIN PROFILE ON ACCOUNT.ID = 222183 AND PROFILE.ACCOUNT_ID = 222183;
	
0.003�b

### ���s�v��̊m�F
#### ���Ȍ���

![���Ȍ����̎��s�v��](plan_selfJoin.png)

#### ��������

![���������̎��s�v��](plan_innerJoin.png)

### �����̎��

#### �N���X���� CROSS JOIN
��̕\�̒��ς�Ԃ��B

    TABLE_A CROSS JOIN TABLE_B

�̃T�C�Y�́A(TABLE_A�̃T�C�Y) * (TABLE_B�̃T�C�Y) �ɂȂ�B

#### �������� INNER JOIN
�����ɍ����s�����Ԃ��B

#### �O������ (LEFT, RIGHT) JOIN
�����ɍ���Ȃ��s���Ԃ��B

    TABLE_A LEFT JOIN TABLE_B

�Ȃ�ATABLE_A�̓��e�͑S�ĕ\������B�����ɍ���Ȃ�TABLE_B�̍s��NULL�ɂȂ�B

    TABLE_A RIGHT JOIN TABLE_B

�Ȃ�ATABLE_B�̓��e�͑S�ĕ\������B�����ɍ���Ȃ�TABLE_A�̍s��NULL�ɂȂ�B

#### ���Ȍ���
AS ���g���āA����e�[�u����ʂ̃e�[�u���Ƃ��čl���Č�������H

#### ���R���� NATURAL JOIN
���l�����������ł���Ă����B�������̂�\���L�[����v���Ă�����̂�Ԃ��H


## �W�v

### ACCOUNT_ID���Ƃ�ALBUM�ɓo�^����Ă��錏�����J�E���g

    SELECT COUNT(*) FROM ALBUM WHERE ACCOUNT_ID=2473261;

���ʁF9

���s�v��͈ȉ��B

![�A���o���o�^�����J�E���g�̎��s�v��](album_count.png)

### �A���o������100���ȏ�̃��[�U�ꗗ���o��
�܂��A�e�A�J�E���g�̃A���o���o�^�����̈ꗗ���擾������@���l�����B

    SELECT ACCOUNT.ID, COUNT(*) 
	FROM ACCOUNT INNER JOIN ALBUM 
	ON ACCOUNT.ID = ALBUM.ACCOUNT_ID 
	GROUP BY ACCOUNT.ID;

�ŁA�ł����B

���ɁA�����

    SELECT * 
	FROM (SELECT ACCOUNT.ID, COUNT(*) CNT FROM ACCOUNT INNER JOIN ALBUM ON ACCOUNT.ID = ALBUM.ACCOUNT_ID GROUP BY ACCOUNT.ID) 
	WHERE CNT >= 100;

�Ƃ���ƁA�A���o������100���ȏ�̃��[�U�ꗗ���o�͂ł����B���s�v��͈ȉ��B

![�A���o��100���ȏ�ꗗ�̎��s�v��](album100.png)




















